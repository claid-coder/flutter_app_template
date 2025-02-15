# Project overview


# Feature requirements


# Frontent Project Structure

각 기능별 폴더는 MVVM 패턴에 따라 View, ViewModel, 관련 Widget들을 포함합니다.

```
lib/
├── app/                    # 앱 초기화 및 설정
│   ├── app.dart
│   └── routes.dart
├── data/                   # 데이터 계층
│   ├── dummy/
│   ├── models/            # 데이터 모델
│   ├── repositories/      # 저장소
│   └── services/          # 외부 서비스
├── presentation/          # UI 계층
│   ├── shared/           # 공통 위젯
│   ├── auth/             # 인증 관련
│   ├── home/             # 메인 화면
│   │   ├── home_view.dart
│   │   ├── home_view_model.dart
│   │   └── widgets/
└── utils/                 # 유틸리티
    ├── constants.dart
    ├── theme.dart
    └── helpers.dart
```

## Data Models

### User
```dart
class User {
  String uid;
  String email;
  String name;
}
```

# Rules

## 코딩 규칙

1. 명명 규칙
   - 클래스: PascalCase
   - 변수/메서드: camelCase
   - 상수: UPPER_SNAKE_CASE

2. 파일 구조
   - 한 파일당 한 클래스
   - 관련 위젯은 widgets/ 하위 폴더에 배치
   - 모든 화면은 view와 view_model 분리

3. 상태 관리
   - Provider 사용
   - ViewModel에서 상태 관리
   - 비즈니스 로직은 Repository에 위임

4. UI/UX
   - Material Design 3 가이드라인 준수
   - 반응형 디자인 필수
   - 다크 / 라이트 모드 지원

## Git 규칙

- 브랜치: feature/, bugfix/, release/ 접두사 사용
- 커밋 메시지: feat:, fix:, docs:, style:, refactor: 등 사용
- PR 전 자체 코드 리뷰 필수

# UI/UX Design Guide

## Design System

### Colors
- Primary: #4CAF50 (건강한 녹색)
- Secondary: #2196F3 (상쾌한 파랑)
- Background: #FFFFFF (화이트)
- Surface: #F5F5F5 (밝은 그레이)
- Text:
  - Primary: #212121 (진한 그레이)
  - Secondary: #757575 (중간 그레이)
- Accent:
  - Success: #66BB6A (연한 녹색)
  - Warning: #FFA726 (주황)
  - Error: #EF5350 (빨강)

### Typography
- Font Family: Pretendard
- Headings
  - H1: Pretendard / 24sp / Bold
  - H2: Pretendard / 20sp / SemiBold
  - H3: Pretendard / 18sp / SemiBold
- Body
  - Body1: Pretendard / 16sp / Regular
  - Body2: Pretendard / 14sp / Regular
- Caption: Pretendard / 12sp / Regular

### Components
- Buttons
  - Primary: 둥근 모서리, Filled
  - Secondary: Outlined
  - Text Button: 원형 배경의 아이콘
- Cards
  - 부드러운 그림자, 8dp 라운드 코너
  - Elevation: 2dp
  - Corner Radius: 8dp
- Bottom Navigation
  - Height: 56dp
  - Icon + Label
- 입력 필드
  - Outlined 스타일, 포커스 시 색상 변경
- 바텀 시트
  - 둥근 상단 모서리, 드래그 핸들 포함

## Screen Layouts

필요한 각 씬마다 Screen Layouts를 작성합니다

### 1. 온보딩 화면
- 스플래시 화면
  - 앱 로고 애니메이션
- 사용자 정보 입력 (4단계)
  1. 기본 정보 (이름, 나이, 성별)
  2. 신체 정보 (키, 체중)
  3. 활동량 선택 (슬라이더)
  4. 목표 설정 (체중 감량/증량/유지)
- 진행 상태 표시 (Progress Bar)

### 2. 로그인 화면

### 3. 홈 화면

# Development plan & checklist

## Phase 1: 프로젝트 초기 설정

- [ ] 프로젝트 구조 설정
  - [ ] MVVM 아키텍처 기본 구조 구현
  - [ ] 디렉토리 구조 설정
  - [ ] 기본 파일 생성
- [ ] 라우팅 설정
  - [ ] 네비게이션 시스템 구축 (go_router)
  - [ ] 라우트 정의
- [ ] 기본 UI, 테마 및 디자인 시스템 설정
  - [ ] 색상 테마 정의
  - [ ] 타이포그래피 설정
  - [ ] 공통 위젯 스타일 정의
- [ ] 필수 의존성 패키지 설정
  - [ ] pubspec.yaml 구성
  - [ ] 외부 라이브러리 설정
- [ ] Firebase 세팅

## Phase 2: 데이터 레이어 구현

- [ ] API 서비스 인터페이스 정의 (Gemini API, Firebase)
  - [ ] REST API 엔드포인트 정의
  - [ ] API 응답 모델 정의
- [ ] 데이터 모델 구현
  - [ ] 엔티티 클래스 정의
  - [ ] 모델 매퍼 구현
- [ ] Repository 패턴 구현
  - [ ] 저장소 인터페이스 정의
  - [ ] 실제 구현체 Impl
- [ ] 로컬 데이터베이스 설정
  - [ ] 데이터베이스 스키마 정의
  - [ ] CRUD 작업 구현

## Phase 3: 홈 화면 개발

- [ ] 데이터 모델 및 더미 데이터 구현
  - [ ] 프로모션 배너 모델 구현
  - [ ] 더미 데이터 추가
  - [ ] 홈 화면 ViewModel 구현
- [ ] 성능 최적화
  - [ ] 이미지 캐싱 구현
  - [ ] 리스트 아이템 재사용
  - [ ] 스크롤 성능 최적화

## Phase 6: 일반 서비스 강화

- [ ] 구독 모델 구현
- [ ] 다국어 지원

## Phase 7: 성능 최적화

- [ ] 이미지 로딩 최적화
- [ ] 리스트 렌더링 성능 개선
- [ ] 메모리 사용량 최적화
- [ ] 앱 시작 시간 최적화

## Phase 8: 테스트 및 품질 관리

- [ ] 단위 테스트 작성
- [ ] 통합 테스트 작성
- [ ] UI/UX 테스트
- [ ] 성능 테스트

## Phase 9: 최종 점검 및 배포 준비

- [ ] 코드 리팩토링
- [ ] 문서화 완료
- [ ] 버그 수정
- [ ] 배포 준비
