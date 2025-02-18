## Docs 구체화에 실제 사용한 스크립트

아래와 같은 앱 서비스를 만들려고 한다. 아래 내용들을 prd.md 의 양식과 예시를 참고하여 작성하라.
@prd.md 의 markdownd 요소 중 '#'으로 시작하는 헤더는 고정한다. '#'이 없는 경우 기존 내용을 충실하게 참고하여 수정하라.


@02_prd.md   를 기반으로 @03_frontend.md  을 작성하고자 한다. @03_frontend.md  에 써있는 기존의 양식과 예시를 참고하여 작성하라. @03_frontend.md  의 markdownd 요소 중 '#'으로 시작하는 헤더는 될 수 있으면 고정한다. '#'이 없는 경우 기존 내용을 충실하게 참고하여 수정해줘.

@02_prd.md  @03_frontend.md  를 기반으로 @04_database.md  을 작성하고자 한다. @02_prd.md  @03_frontend.md  에 써있는 기존의 양식과 예시를 참고하여 작성하라. @04_database.md  의 markdownd 요소 중 '#'으로 시작하는 헤더는 될 수 있으면 고정한다. '#'이 없는 경우 기존 내용을 충실하게 참고하여 수정해줘.

@03_frontend.md  @04_database.md  에 다른 Model의 요소를 ChatRoom Model로 분리하고 반영해줘

[Instruction]
아래와 같은 앱 서비스를 만들려고 한다. 아래 내용들을 @prd.md 의 양식과 예시를 참고하여 작성하라.
@prd.md 의 markdownd 요소 중 '#'으로 시작하는 헤더는 고정한다. '#'이 없는 경우 기존 내용을 충실하게 참고하여 수정해줘.

[서비스 내요]
앱 서비스 명 : Interactive Novel
앱 서비스 설명
- 이 앱은 소설과 같은 상품이 존재한다. 고객은 이 소설을 선택하여 데모 버전을 이용한 후, 일정 대화 이후 유료 결재 할 수 있다.
- 이 'Interactive Novel'에는 해당 캐릭터의 패르소나와 이야기 세계관, 이야기 시퀀스를 System Prompt 혹은 RAG로 입력되어 있다.
- 이 'Interactive Novel'은 TRPG와 같이 스탯 정보가 갈 수도 있고, 추리게임처럼 주변 상황이 기술될 수도 있다.
- 이 'Interactive Novel'은 이미지, GIF, 동영상, 음성 파일과 같이 제공 될 수 있다.
- 사용자가 Text를 입력했을때, 구조화된 문서로 LLM에게 전달한다. 구조화된 문서에는 스토리 진행에 필요한 정보가 들어있다.
- ChatGPT와 같은 LLM이 구조화 된 답변으로(json) 'Interactive Novel'의 컨텐츠를 이용하여 답변해준다.

[구체화 된 앱 서비스]
```
# PoC 구현 내용
## 로그인
- 하단 버튼들 : OAuth를 활용한 로그인 제공 (Google, Apple)
- 넷플릭스, 네이버 시리즈와 유사한 소설들 배열
## 온 보딩 프로세스
- 본 서비스에 대한 단계별 설명
- 추천 소설을 제공하기 위한 고객의 정보 수집 : 성별, 나이, 좋아하는 장르
## 홈 화면
- Firebase store에 올라간 추천하는 소설 리스트는 Firebase에서 얻어옴
  - **추천 소설리스트 Model, Data 필요**
    - 최근에 사용자가 읽은 소설들
    - 같은 취향의 독자들이 읽는 소설 : 사용자 정보와 최근 읽은 소설을 기반으로
    - 최신 소설
- 소설을 누르면 소설 소개 화면으로 넘어감
- 상단 바에 포인트 조회, 알림, 설정 아이콘
- 하단 탭에 홈, 검색, 이벤트, 보관함(최근에 본 / 대여, 소장한 / 관심 / 다운로드 내역)
## 소설 소개 화면
- 소설 표지 및 썸네일, 소설 제목
- 소설의 소개, 소설의 작성자
- 소설의 인기도 : 독자수, 다운로드 수, 읽은 독자의 추천 점수(star),
- 작가 공지사항
- 예상 진행시간
- '이야기 진행' 버튼 : 해당 Interactive Novel을 시작
- 이야기 구매 버튼
- **소설 별정보 Model 필요**
## 설정
- 사용자 프로필 설정 버튼 -> 사용자 설정
- 소설 앱의 테마(다크, 라이트, 시스템)
- 다운로드한 소설 관리 
## 결제 화면
- 해당 Interactive Novel에 대해 결재
- 금액, 구매 주의사항, 구매 버튼 표시

# 테마 및 디자인
- 젊은 사람들이 좋아하는 세련된 디바인과 색 배합 지정
- 라이트, 다크, 시스템 테마 제공
- lib/app/app_theme.dart 에 모두 구현

# Backlogs : PoC 단계에서 구현하지 않아도 됨
- 자세한 사용자 프로필 설정 화면
- 자세한 설정
  - 기기 등록 관리, 이동통신망 사용 알림
- 실제 결제 프로세스
```

@prd.md Project structure 에 전체적으로 수정이 필요해
이야기 요소의 모음(이야기 파일, 이미지, 영상, 음성 파일 등)이 챕터마다 암호화 된 압축파일로 firebase store에 있고,
이야기의 챕터마다 압축을 풀어서 임시로 앱 내 임시로 압축을 풀어두고 사용한다.
따라서, class Novel에는 gameStats이 존재하지 않는다. class Novel에는 NovelChapter들의 이름과 주소가 순서대로 list로 있을 수 있다.
이에따라 NovelChapter model을 만들고,  StoryProgress를 재설계하라.
기타 재설계가 필요한 부분도 제안하라

@prd.md 에 사용자가 앱을 껐다가 켜도 동작하도록 세이브 파일을 만들려고 한다.
@prd.md 을 참고하여 StorySave 구조에 대한 모델을 만들어라.

@prd.md 에 List나 Map 구조체 혹은 설명이 필요한 String은 각 구조 아래에 예시를 들어라

@prd.md 의 서로 다른 내용을 참고하여, 업데이트 된 내용을 @prd.md 의 다른 곳에도 업데이트 하라

@prd.md 에 있는 List나 Map 구조체 혹은 설명이 필요한 Class, String, Enum은 각 구조 아래에 예시를 들어라.
수정이 필요하면 수정하라.
NovelType
Map<String, dynamic> gameState;  // 현재 게임 스탯, 플래그 등
Map<String, String> resourceStates;  // 리소스별 상태 정보

@prd.md 에 필요한 라이브러리 있으면 추천해줘
avatar_glow 같은 효과, 이펙트 라이브러리도 추가해줘

@prd.md 를 기반으로 @frontend.md 을 작성하고자 한다. @frontend.md 에 써있는 기존의 양식과 예시를 참고하여 작성하라.
@frontend.md 의 markdownd 요소 중 '#'으로 시작하는 헤더는 고정한다. '#'이 없는 경우 기존 내용을 충실하게 참고하여 수정해줘.

@prd.md 를 Project structure 기반으로 @frontend.md 에 적당한 곳에 주요 컴포넌트 설명을 추가하라

@prd.md @frontend.md 를 기반으로 @database.md 을 작성하고자 한다. @database.md 에 써있는 기존의 양식과 예시를 참고하여 작성하라.
@database.md 의 markdownd 요소 중 '#'으로 시작하는 헤더는 고정한다. '#'이 없는 경우 기존 내용을 충실하게 참고하여 수정해줘.

@02_prd.md @firebase_install_nodejs.md @firebase_setting_function.md 를 바탕으로  @05_firebase_functions.md 에 # 헤더에 따라 아주 자세히 구체화하라