# Troubleshooting

## Android

### compileDebugJavaWithJavac 에러 (gradle 버전 문제)

compileDebugJavaWithJavac 같은 문제가 발생했을 경우 '해결 방법'을 참고하여 해결할 수 있습니다.
```
Launching lib/main.dart on SM-S928N in debug mode...
Running Gradle task 'assembleDebug'...

FAILURE: Build failed with an exception.

* What went wrong:
  Execution failed for task ':shared_preferences_android:compileDebugJavaWithJavac'.
> Could not resolve all files for configuration ':shared_preferences_android:androidJdkImage'.
> Failed to transform core-for-system-modules.jar to match attributes {artifactType=_internal_android_jdk_image, org.gradle.libraryelements=jar, org.gradle.usage=java-runtime}.
> Execution failed for JdkImageTransform: /Users//Library/Android/sdk/platforms/android-34/core-for-system-modules.jar.
```

#### compileDebugJavaWithJavac 해결 방법
1. Upgrade Gradle version:  
   To support JDK 21, you'll need at least Gradle 8.5. You can check the [Java Compatibility](https://docs.gradle.org/current/userguide/compatibility.html#java_runtime) for more details.
   Update your `android/gradle/wrapper/gradle-wrapper.properties` file like this:
```ini
distributionUrl=https\://services.gradle.org/distributions/gradle-8.5-all.zip
```

2. Upgrade AGP version:  
   In my testing, to work with JDK 21 and Gradle 8.5, you'll need at least AGP 8.3.
   Update your `android/settings.gradle` file like this:
```groovy
plugins {
    id "com.android.application" version "8.3.0" apply false
}
```

### INSTALL_FAILED_INSUFFICIENT_STORAGE 오류
Android 에뮬레이터의 저장 용량이 부족하면 나옵니다.

아래 내용 따라서 용량을 늘려주니 오류가 없어지네요
(userdata-qemu.img 파일까지 찾아서 삭제해야 용량이 늘어나네요)

출처: https://ssue-dev.tistory.com/21
```
Requested internal only, but not enough space
```

#### INSTALL_FAILED_INSUFFICIENT_STORAGE 해결 방법
1. 에뮬레이터 설정에서 변경
  - 안드로이드 스튜디오에서 에뮬레이터 설정 열기
  - "Show Advanced Settings" 클릭
  - "Memory and Storage" 섹션에서 "Internal Storage" 값 조정
  - 에뮬레이터 재시작하여 변경사항 적용

2. 수동으로 초기화 (설정 변경이 안될 경우)
  - 디바이스 매니저에서 해당 에뮬레이터의 "Show on Disk" 선택
  - "userdata-qemu.img" 파일 삭제
  - 에뮬레이터 재시작
    - 주의: 이 방법은 에뮬레이터를 초기화하므로 기존 앱과 데이터가 모두 삭제됨

### 앱에서 YouTube 음악이 안나온다면
youtube_player_flutter 패키지를 사용할 때 알아야 할 중요한 점

1. 영상과 음악은 함께 재생됨
  이 패키지는 유튜브 영상과 음악을 재생할 수 있는 도구입니다.
    주의 : 영상이 정상적으로 화면에 보여야만 음악도 함께 재생됩니다.
  즉, 영상 없이 음악만 들리게 만드는 것은 안 됩니다.

2. 화면에 영상 구현 방법
  앱 화면에 유튜브 플레이어를 추가하세요.
  유튜브 영상을 표시할 공간(위젯)을 만들어야 음악도 정상적으로 재생됩니다.

## iOS

### error (xcode): unsupported option '-g' for target 'arm64-apple-ios13.0-simulator'
https://medium.com/@abul_8793/error-xcode-unsupported-option-g-for-target-arm64-apple-ios10-0-1bd2af0d5b07
https://sj-d.tistory.com/55

```
파일 위치: /rootProject/ios/Podfile
post_install 블록에 아래 코드를 추가합니다

post_install do |installer|
  installer.generated_projects.each do |project|
    project.targets.each do |target|
      target.build_configurations.each do |config|
        config.build_settings['IPHONEOS_DEPLOYMENT_TARGET'] = '13.0'
      end
    end
  end

  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
  end

  # Xcode 16 임시추가 부분
  installer.pods_project.targets.each do |target|
    if target.name == 'BoringSSL-GRPC'
      target.source_build_phase.files.each do |file|
        if file.settings && file.settings['COMPILER_FLAGS']
          flags = file.settings['COMPILER_FLAGS'].split
          flags.reject! { |flag| flag == '-GCC_WARN_INHIBIT_ALL_WARNINGS' }
          file.settings['COMPILER_FLAGS'] = flags.join(' ')
        end
      end
    end
  end
  # Xcode 16 임시추가 부분
end
```

### Lexical or Preprocessor Issue (Xcode): Include of non-modular header inside framework module 'firebase_auth
https://github.com/firebase/flutterfire/issues/13342
https://stackoverflow.com/questions/66148505/flutter-include-of-non-modular-header-inside-framework-module-firebase-core-fl
```
You have to go to Xcode => Runner => Build Settings => All => Apple Clang-Language-Modules
and put "Allow Non-modular Includes In Framework Modules" to "yes"
```

https://github.com/flutter/flutter/issues/154783
https://github.com/firebase/flutterfire/issues/12993#issuecomment-2188776541
```
flutter clean
rm -rf pubspec.lock ios/Podfile.lock ios/Pods/
```

```
platform :ios, '13.0'
...
post_install do |installer|
  installer.pods_project.targets.each do |target|
    flutter_additional_ios_build_settings(target)
    target.build_configurations.each do |config|
      # Allow Non-modular Includes In Framework Modules 설정
      config.build_settings['CLANG_ALLOW_NON_MODULAR_INCLUDES_IN_FRAMEWORK_MODULES'] = 'YES'
    end
  end
end
```

change xcode config
1. open ios/Runner.xcodeproj with xcode
2. click project -> Runner -> Build Settings
3. in search bar: Allow Non-modular Includes in Framework Modules and changer Runner to yes.

```
flutter pub get
cd ios/
pod install
```

### Flutter + Firestore 빌드 속도 느림

https://origogi.github.io/flutter/github-actions-ios/
https://velog.io/@kji0205/Firestore-%ED%8C%A8%ED%82%A4%EC%A7%80-%EC%B6%94%EA%B0%80%ED%95%A0%EB%95%8C-iOS-%EB%B9%8C%EB%93%9C-%EC%86%8D%EB%8F%84-%EC%A4%84%EC%9D%B4%EB%8A%94-%EB%B2%95

ios/Potfile
```
target 'Runner' do
  # Pre-build 된 Firestore 라이브러리를 직접 사용
  # pod 'FirebaseCore', :git => 'https://github.com/invertase/firestore-ios-sdk-frameworks.git', :tag => '10.25.0'
  pod 'FirebaseFirestore', :git => 'https://github.com/invertase/firestore-ios-sdk-frameworks.git', :tag => '10.25.0'
  # pod 'FirebaseMessaging', :git => 'https://github.com/invertase/firestore-ios-sdk-frameworks.git', :tag => '10.25.0'

  use_frameworks!
  use_modular_headers!

  flutter_install_all_ios_pods File.dirname(File.realpath(__FILE__))
  target 'RunnerTests' do
    inherit! :search_paths
  end
end
```

### CocoaPods's specs repository is too out-of-date to satisfy dependencies.

```
Error: CocoaPods's specs repository is too out-of-date to satisfy dependencies.
To update the CocoaPods specs, run:
  pod repo update
```
ios/Podfile.lock 를 삭제
pod install --repo-update

```
% pod install --repo-update
Updating local specs repositories
Analyzing dependencies
Pre-downloading: `FirebaseFirestore` from `https://github.com/invertase/firestore-ios-sdk-frameworks.git`, tag `10.25.0`
cloud_firestore: Using Firebase SDK version '11.6.0' defined in 'firebase_core'
firebase_auth: Using Firebase SDK version '11.6.0' defined in 'firebase_core'
firebase_core: Using Firebase SDK version '11.6.0' defined in 'firebase_core'
firebase_storage: Using Firebase SDK version '11.6.0' defined in 'firebase_core'
[!] CocoaPods could not find compatible versions for pod "FirebaseCoreExtension":
  In Podfile:
    FirebaseFirestore (from `https://github.com/invertase/firestore-ios-sdk-frameworks.git`, tag `10.25.0`) was resolved to 10.25.0, which depends on
      FirebaseFirestoreBinary (= 10.25.0) was resolved to 10.25.0, which depends on
        FirebaseCoreExtension (= 10.25.0)

    firebase_auth (from `.symlinks/plugins/firebase_auth/ios`) was resolved to 5.4.1, which depends on
      Firebase/Auth (= 11.6.0) was resolved to 11.6.0, which depends on
        FirebaseAuth (~> 11.6.0) was resolved to 11.6.0, which depends on
          FirebaseCoreExtension (~> 11.6.0)
```

프로젝트에서 사용하는 firebase_core, firebase_auth, cloud_firestore 등 FlutterFire 플러그인들의 버전이 서로 호환되는지 확인해 보세요.
FlutterFire 버전 호환성 매트릭스를 참고하여 버전을 조정할 수 있습니다.
https://github.com/firebase/flutterfire/blob/main/VERSIONS.md
또는 FlutterFire 플러그인 pub.dev 페이지에서 확인 가능

아래 Pre-build 된 Firestore 라이브러리를 사용하는 부분 주석 처리하고 빌드 한 번 시도

ios/Potfile
```
target 'Runner' do
  # Pre-build 된 Firestore 라이브러리를 직접 사용
  # pod 'FirebaseCore', :git => 'https://github.com/invertase/firestore-ios-sdk-frameworks.git', :tag => '10.25.0'
  # pod 'FirebaseFirestore', :git => 'https://github.com/invertase/firestore-ios-sdk-frameworks.git', :tag => '10.25.0'
  # pod 'FirebaseMessaging', :git => 'https://github.com/invertase/firestore-ios-sdk-frameworks.git', :tag => '10.25.0'

  use_frameworks!
  use_modular_headers!

  flutter_install_all_ios_pods File.dirname(File.realpath(__FILE__))
  target 'RunnerTests' do
    inherit! :search_paths
  end
end
```

## Etc

### flutter_dotenv 사용법
https://velog.io/@false90/Flutterenv%EB%A1%9C-API-Key%EB%A5%BC-%EA%B0%80%EB%A0%A4%EB%B3%B4%EC%95%84%EC%9A%94

```shell
flutter pub add flutter_dotenv
```

pubspec.yaml
```yaml
# The following section is specific to Flutter packages.
flutter:
  uses-material-design: true

  assets:
    - assets/images/
    - .env ←
```

.env
```sh
# .gitignore에 추가 필수! (gitignore는 cursorignore임)
GEMINI_API_KEY="YOUR_API_KEY"
```

lib/main.dart
```dart
import 'package:flutter_dotenv/flutter_dotenv.dart';

void main() async {
  // Flutter 바인딩 초기화
  WidgetsFlutterBinding.ensureInitialized();

  // .env 파일 로드
  await dotenv.load(fileName: '.env');

  // Firebase 초기화
...
}
```

lib/data/services/gemini_service.dart
```dart
import 'package:flutter_dotenv/flutter_dotenv.dart';

class GeminiService {
  static final String _apiKey = dotenv.env['GEMINI_API_KEY'] ?? '';
...
}
```

## Flutter - 앱 권한 관리하기(permission_handler)
https://velog.io/@error/Flutter-%EC%95%B1-%EA%B6%8C%ED%99%98-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0

voice_chat에서는 permission_handler 사용 안하고도 풀리는 문제였음