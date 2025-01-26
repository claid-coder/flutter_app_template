# Documents

@frontend.md 파일의 "5. 테마 지원 / Phase 9: 테마 시스템 개선"을 구체화 해주세요.
- 구체화 된 내용을 "Feature requirements"에 업데이트 해주세요. (체크는 하지마세요)
- 구체화 된 내용을 Development plan & status에 업데이트 해주세요. (여기에 체크박스를 만들어주세요)


@frontend.md 와 @database.md 를 기반으로 @prd.md 의 `# 1. Project Overview` 를 업데이트 해주세요. 기존에 작성 된 것도 부족하거나 잘못됐으면 고쳐주세요.
@frontend.md 와 @database.md 를 기반으로 @prd.md 의 `# 2. Core functionalities` 를 개선해주세요. 기존에 작성 된 것도 부족하거나 잘못됐으면 고쳐주세요.

@Codebase 이제까지 진행사항을 @frontend.md에 다음 사항을 수행하세요
- Development plan & status에 현재까지의 진행 사항 업데이트 및 체크해주세요

@Codebase 이제까지 진행사항을 @frontend.md에 다음 사항을 수행하세요
- Feature requirements에는 수정 및 신규 항목만 업데이트 해주세요 (체크는 하지마세요)

lib 폴더의 모든 소스코드 파일들 @frontend.md # File structure 폴더 구조 대로 정리해줘

@database.md 파일에 데이터베이스 구조와 파이어베이스 스토리지 사용에 관한 구조설계를 해줘 md 파일에 맞게 작성해. 우리가 앱에서 구현할 기능은 아래와 같아.
1. 소셜 로그인시 로그인 정보 저장
2. 게시글 업로드시 정보 저장
3. 미디어 파일 업로드시 스토리지에 저장

@database.md 파일에 설계된 데이터 구조를 바탕으로, 이 프로젝트에서 Firebase Firestore와 Storage를 사용하는 각 기능의 구현 계획을 마크다운 형식의 체크 리스트를 추가해주세요. 그리고 이 계획에 따라 작업을 진행해주세요.

@database.md "Firestore 규칙 (유저 정보, 업로드 데이터 등), Firebase Storage 규칙 (미디어 파일 관리), 데이터 관리 지침, 추가 규칙"에 부족한 부분이 있으면 수정 및 업데이트 해줘

# Coding

@frontend.md 파일의 Phase 1을 기반으로 @Codebase 플러터 앱 제작을 시작해주세요. 각 작업이 끝날 때마다 현재 진행 상황을 frontend.md 파일에 업데이트하며 안정적으로 작업을 진행해 주세요.

@frontend.md 파일의 "5. 테마 지원 / Phase 9: 테마 시스템 개선"을 기반으로 @Codebase 플러터 앱 제작을 시작해주세요. 각 작업이 끝날 때마다 현재 진행 상황을 frontend.md 파일에 "Development plan & status"업데이트하며 안정적으로 작업을 진행해 주세요.

아래 작업내용을 기반으로 @Codebase 플러터 앱 제작을 시작해주세요. 각 작업이 끝날 때마다 Development plan & status과 추가된 요소들을 frontend.md 파일에 업데이트하며 안정적으로 작업을 진행해 주세요.
[작업내용]
홈 화면에 콘텐츠 레이아웃을 아래와 같이 작성해줘
- 가장 위에 하이라이트로 큰 사진 슬라이드와 슬라이드 하단 왼쪽에 뉴스 제목 서줘
- '큰 사진 슬라이드' 밑에 뉴스 들을 2열로 배열해줘

아래 작업내용을 기반으로 @Codebase 플러터 앱 제작을 시작해주세요. 각 작업이 끝날 때마다 Development plan & status과 추가된 요소들을 frontend.md 파일에 업데이트하며 안정적으로 작업을 진행해 주세요.
[작업내용]
다크/라이트 테마를 제대로 만들어보고 싶습니다.
지금은 다크 테마 위주로 만들어져 있습니다. 따라서 지금 설정된 색 들은 다크테마 설정 및 constant에 넣어주시고, 세련된 UI의 라이트 테마를 dark 테마의 데이터와 동일하게 만들어 적용해야합니다.

아래 작업내용을 기반으로 @Codebase 플러터 앱 제작을 시작해주세요. 각 작업이 끝날 때마다 Development plan & status과 추가된 요소들을 frontend.md 파일에 업데이트하며 안정적으로 작업을 진행해 주세요.
[작업내용]
News Card나 list item을 터치하면 제목, 이미지, 뉴스 내용을 보여주는 screen이 있었으면 좋겠습니다.

@news_list_section.dart 에서 되도록 많은 뉴스를 보여주기 위해 아래와 같이 배치해
사진 | 카테고리 제목        source |
사진 | 기사 (maxLine==2)         |
사진 |                          |

@news_screen.dart 에서 model/data를 다루지 말고, news_view_model.dart에서 다루도록 수정해

@home_screen.dart 에서 model/data를 다루지 말고, home_view_model.dart에서 다루도록 수정해

