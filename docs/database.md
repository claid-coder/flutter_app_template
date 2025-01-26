# local database 규칙 (sqlite, room, 앱 데이터 등)

## 로컬 데이터베이스 구조 (lib/data/repository)

# firebase database 규칙 (유저 정보, 업로드 데이터 등)

## 원격 데이터베이스 구조 (lib/data/repository)

# firebase storage 규칙 (미디어 파일 관리)

## 스토리지 구조

# 데이터 관리 지침

## Data Rules & Constraints

### 1. 일반 규칙
- 모든 날짜/시간은 UTC milliseconds 형식으로 저장
- 실수형 데이터는 소수점 1자리까지만 저장 (반올림)
- 모든 테이블은 생성 시간(createdAt) 포함

### 2. User Table 규칙
- name: 최소 2자, 최대 20자
- age: 14세 이상, 100세 이하
- gender: "MALE", "FEMALE", "OTHER" 중 하나
- activityLevel: "LOW", "MEDIUM", "HIGH" 중 하나
- goal: "LOSS", "MAINTAIN", "GAIN" 중 하나

### 3. Food Records 규칙
- calories: 0 이상
- 영양소(carbs, protein, fat): 0 이상, 소수점 1자리
- mealType: "BREAKFAST", "LUNCH", "DINNER", "SNACK" 중 하나
- recordDate: 하루 시작은 00:00:00 UTC 기준

### 4. Daily Nutrition 규칙
- 하루에 한 사용자당 하나의 레코드만 존재
- 자동 업데이트: 식사 기록 추가/삭제시 자동 계산
- 모든 영양소 값은 0 이상

## 데이터 마이그레이션 전략

### Version 1 -> 2
```kotlin
val MIGRATION_1_2 = object : Migration(1, 2) {
    override fun migrate(database: SupportSQLiteDatabase) {
        // 마이그레이션 로직
    }
}
```

## 백업 전략
- Room 데이터베이스 파일 자동 백업 활성화
- 최대 7일간의 백업 유지
- 백업 시 Wi-Fi 연결 필요

## 성능 최적화
1. 인덱스 활용
2. 트랜잭션 처리
3. 비동기 쿼리 처리
4. 페이징 처리 (대량 데이터)

# 추가 규칙
