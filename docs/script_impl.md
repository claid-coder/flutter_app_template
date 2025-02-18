# Script 모음

## App 구현에 실제 사용한 스크립트

아래 코드를 예시로 @app.dart @routes.dart 를 작성하라

```dart
이전에 구현한 routes.dart 코드
```

@frontend.md 와 아래 코드를 참고하여 이 앱에 어울리는 @theme.dart 를 작성하시오

```dart
이전에 구현한 theme 코드
```

@03_frontend.md @02_prd.md 를 참고하여 @theme.dart 에 알맞은 테마 색과 수치를 업데이트 해라. 전체적인 코드 구조는 유지하라

@routes.dart 를 기반으로 presentation 스켈레톤을 작성하고, 기본적인 view를 구현하라

로그인 화면을 만들어보자. 로그인 화면은 @splash_view.dart  가 끝나면 글자가 슬라이드 되어 사라지고,
route로 지금과 같은 배경에 @login_view.dart  로그인 버튼이 나타나는 거야.
로그인 버튼들은 아래를 참고해

```
SizedBox(
  width: double.infinity,
  child: ElevatedButton.icon(
    onPressed: viewModel.isLoading
        ? null
        : () => viewModel.signInWithGoogle(context),
    icon: viewModel.isLoading
        ? const SizedBox(
            width: 24,
            height: 24,
            child: CircularProgressIndicator(),
          )
        : const FaIcon(FontAwesomeIcons.google,
            color: Colors.red),
    label: Text(
      viewModel.isLoading ? '로그인 중...' : 'Google로 시작하기',
    ),
    style: ElevatedButton.styleFrom(
      padding: const EdgeInsets.symmetric(
          horizontal: 24, vertical: 12),
      backgroundColor: Colors.white,
      foregroundColor: Colors.black87,
    ),
  ),
),
const SizedBox(height: 16),
SizedBox(
  width: double.infinity,
  child: ElevatedButton.icon(
    onPressed: () => viewModel.signInWithApple(context),
    icon: const FaIcon(FontAwesomeIcons.apple),
    label: const Text('Apple로 시작하기'),
    style: ElevatedButton.styleFrom(
      padding: const EdgeInsets.symmetric(
          horizontal: 24, vertical: 12),
      backgroundColor: Colors.black,
      foregroundColor: Colors.white,
    ),
  ),
),
```

@home_view.dart 에서는 지금 테마 적용해주고,
@02_prd.md 에 적힌 ## 홈 화면의 스켈레톤 presenation을 적용해줘

@home_view.dart 에 추천 캐릭터 목록의 아이템들을 카드 형태로 만들어줘
인기 캐릭터, 신규 캐릭터, 사용자 맞춤 추천 섹션도 만들어줘

자 _buildCharacterSection에 들어갈 각 요소들을 data/dummy 폴더에 임시로 만들거야.
dummy를 만들기 위해서 data/repository, data/model을 먼저 만들어줘야겠지?


---

## 구체화

@frontend.md 파일의 "5. 테마 지원 / Phase 9: 테마 시스템 개선"을 구체화 해주세요.
- 구체화 된 내용을 "Feature requirements"에 업데이트 해주세요. (체크는 하지마세요)
- 구체화 된 내용을 Development plan & status에 업데이트 해주세요. (여기에 체크박스를 만들어주세요)

@prd.md 위 내용을 바탕으로 PRD 문서를 마크다운 형식으로 작성해 주세요.
1. @prd.md 에 써있는 양식과 예시를 기반으로 작성하세요.
2. Firebase Functions를 사용하여 API를 호출할 예정입니다.
3. MVVM 패턴을 이용하여 파일 구조를 계획해 주세요.
4. 모든 데이터는 로컬에 저장하여 사용할 계획입니다.
5. 파이어베이스를 이용한 소셜 로그인을 통해 유저 정보를 기록하고 로컬 데이터에 저장하고 관리 할 계획입니다. (다른 서비스는 이용하지 않음)

@prd.md의 내용을 바탕으로 @frontend.md 문서를 마크다운 형식으로 작성해 주세요.
1. UI/UX 디자이너의 관점에서 최대한 현대적이고 깔끔한 디자인을 구상해 주세요.
2. 사용자가 쉽게 이용하고 직관적으로 이해할 수 있는 구조로 만들어 주세요.
3. MVVM 패턴으로 설계해 주세요.
4. 작업 순서에 따른 체크리스트를 만들어 주세요.

@database.md 파일에 database 구조와 firebase storage 구조설계를 해서 @database.md 파일에 맞게 작성해.
우리가 앱에서 구현할 기능은 아래와 같아.
1. 소셜 로그인시 로그인 정보 저장
2. 게시글 업로드시 정보 저장
3. 미디어 파일 업로드시 스토리지에 저장

@prd.md 와 @frontend.md 문서를 참고하여 @database.md 를 마크다운 형식으로 작성해주세요
1. 데이터는 로컬에 저장 할 예정입니다.
2. 해당 문서들을 기반으로 효율적인 데이터 구조를 만들어주세요
3. 데이터베이스의 규칙을 설정하여 일관성을 유지하세요

@frontend.md 문서를 바탕으로 @Codebase 앱의 프론트엔드 구현 작업만 먼저 실행해주세요. 작업이 마무리되면 항상 이 문서를 업데이트하는 방식으로 진행해 주세요.
가능하다면 한 세션에서 3~4개의 작업을 완료해주세요.

@frontend.md 작업이 완료될 때마다 체크리스트를 업데이트하며 진행하세요

## 진행사항 업데이트
@Codebase 이제까지 진행사항을 @frontend.md 'Development plan & Checklist'에 현재까지 진행 사항 업데이트 및 체크해주세요
@Codebase 이제까지 진행사항을 @frontend.md에 'Feature requirements'에는 상이한 부분 수정 및 신규 항목만 써주세요 (체크 없이)

@frontend.md 와 @database.md 를 기반으로
@prd.md 의 `# 1. Project Overview` 를 업데이트 해주세요. 기존에 작성 된 것도 부족하거나 잘못됐으면 고쳐주세요.
@frontend.md 와 @database.md 를 기반으로
@prd.md 의 `# 2. Core functionalities` 를 개선해주세요. 기존에 작성 된 것도 부족하거나 잘못됐으면 고쳐주세요.

lib 폴더의 모든 소스코드 파일들 @frontend.md # File structure 폴더 구조 대로 정리해줘

@database.md 파일에 설계된 데이터 구조를 바탕으로,
이 프로젝트에서 Firebase Firestore와 Storage를 사용하는 각 기능의 구현 계획을 마크다운 형식의 체크 리스트를 추가해주세요.
그리고 이 계획에 따라 작업을 진행해주세요.

@database.md "Firestore 규칙 (유저 정보, 업로드 데이터 등), Firebase Storage 규칙 (미디어 파일 관리), 데이터 관리 지침, 추가 규칙"에 부족한 부분이 있으면 수정 및 업데이트 해주세요

# Programming

@frontend.md 문서를 바탕으로 @Codebase 앱의 프론트엔드 구현 작업만 먼저 실행해주세요. 작업이 마무리되면 항상 이 문서를 업데이트하는 방식으로 진행해 주세요.
가능하다면 한 세션에서 3~4개의 작업을 완료해주세요.

@frontend.md 파일의 Phase 1을 기반으로 @Codebase 플러터 앱 제작을 시작해주세요.
각 작업이 끝날 때마다 현재 진행 상황을 frontend.md 파일에 업데이트하며 안정적으로 작업을 진행해 주세요.

아래 작업내용을 기반으로 @Codebase 플러터 앱 제작을 시작해주세요.
각 작업이 끝날 때마다 Development plan & status과 추가된 요소들을 frontend.md 파일에 업데이트하며 안정적으로 작업을 진행해 주세요.
[작업내용]
홈 화면에 콘텐츠 레이아웃을 아래와 같이 작성해줘
- 가장 위에 하이라이트로 큰 사진 슬라이드와 슬라이드 하단 왼쪽에 뉴스 제목 서줘
- '큰 사진 슬라이드' 밑에 뉴스 들을 2열로 배열해줘

@news_list_section.dart 에서 되도록 많은 뉴스를 보여주기 위해 아래와 같이 배치해
```
사진 | 카테고리 제목        source |
사진 | 기사 (maxLine==2)         |
사진 |                          |
```

@news_screen.dart 에서 model/data를 다루지 말고, news_view_model.dart에서 다루도록 수정해

@firebase.options.dart 를 이용해 로그인 페이지를 구현하고 로그인이 완료 되면 온보딩 페이지가 나타나게 해주세요,
온보딩 페이지에 식습관과 개인 건강정보(알레르기, 기저질환 등)를 입력할 수 있는 페이지를 만들고,
@frontend.md와 @database.md 에 각각 내용을 추가 하세요.

# Images

## https://copilot.microsoft.com/chats

심플한 스타일로 그려주고, 사람 손 그리지마. 선이 흐트러지지 않게 정교하게.
건강을 위한 과학적인 데이터 분석을 상단 배너 그림으로 그려줘.
가운데에 전신 그림 아주 아주 작게 그려줘.
