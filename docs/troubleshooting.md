# Troubleshooting

## compileDebugJavaWithJavac 에러 (gradle 버전 문제)

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

### compileDebugJavaWithJavac 해결 방법
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

## INSTALL_FAILED_INSUFFICIENT_STORAGE 오류
Android 에뮬레이터의 저장 용량이 부족하면 나옵니다.

아래 내용 따라서 용량을 늘려주니 오류가 없어지네요
(userdata-qemu.img 파일까지 찾아서 삭제해야 용량이 늘어나네요)

출처: https://ssue-dev.tistory.com/21
```
Requested internal only, but not enough space
```

### INSTALL_FAILED_INSUFFICIENT_STORAGE 해결 방법
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

## 앱에서 YouTube 음악이 안나온다면
youtube_player_flutter 패키지를 사용할 때 알아야 할 중요한 점

1. 영상과 음악은 함께 재생됨
  이 패키지는 유튜브 영상과 음악을 재생할 수 있는 도구입니다.
    주의 : 영상이 정상적으로 화면에 보여야만 음악도 함께 재생됩니다.
  즉, 영상 없이 음악만 들리게 만드는 것은 안 됩니다.

2. 화면에 영상 구현 방법
  앱 화면에 유튜브 플레이어를 추가하세요.
  유튜브 영상을 표시할 공간(위젯)을 만들어야 음악도 정상적으로 재생됩니다.
