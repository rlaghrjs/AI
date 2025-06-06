<!-- info -->
### 인공지능 미니프로젝트


<!-- introduce -->
## 📌 문제정의

- 서울 자전거 공유 수요 데이터를 활용한 여러 조건에 따른 자전거 대여량 확인 모델
- 정형데이터회귀
- 입력변수 : 날짜, 시간, 온도(C), 습도(%), 풍속(m/s), 강수량(mm), 강설량(cm), 계절, 공휴일여부, 운영일여부	
- 출력변수 : 자전거 대여 수


## 📊 데이터설명
- 데이터 출처 : https://archive.ics.uci.edu/dataset/560/seoul+bike+sharing+demand
- 총 데이터 개수 : 8760개
- 속성 : 14개
- 데이터 비율:
  - 훈련데이터 : 70퍼
  - 테스트데이터 : 30퍼
  - 검증데이터 : 훈련데이터의 25퍼

## 🧹 전처리 과정

- 'Date' 데이터를 'datetime' 타입으로 변경
- sin, cos함수를 이용하여 'Hour', 'Month' 데이터의 순환성 표시
- 'Weekday' 데이터의 각 요일을 숫자로 변환하고 주말 여부를 0과 1로 구분
- 'Holiday', 'Functioning day'는 0과 1로 구분 가능하게 변경
- 'Seasons', 'Weekday'는 원핫 인코딩 처리

## ⚙️ 사용된 옵션

- 은닉층 활성화 함수+ : ReLU
- Optimizer : adam
- 평가지표 : MSE

## 🔍 하이퍼 파라미터 최적화 결과 

- 배치사이즈 변경

| 번호 | 배치사이즈| 뉴런 개수 | 드롭아웃층 | MSE |
|------|-----------|-----------|------------|-----|
| 1    | 32        | 64, 32    | X           | 69862 |
| 2    | 16        | 64, 32    | X           | 81249 |
| 3    | 64        | 64, 32    | X           | 75429 |

- 뉴런 개수 변경

| 번호 | 배치사이즈| 뉴런 개수 | 드롭아웃층 | MSE |
|------|-----------|-----------|------------|-----|
| 1    | 32        | 128, 64, 32  | X           | 64537 |
| 2    | 32        | 256, 128, 64 | X           | 57894 |
| 3    | 32        | 64, 32, 16   | X           | 73604 |

- 드롭아웃층 추가

| 번호 | 배치사이즈| 뉴런 개수 | 드롭아웃층 | MSE |
|------|-----------|-----------|------------|-----|
| 1    | 32        | 256, 128, 64  | X           | 68024 |

## 최종 모델 성능

- 배치사이즈 : 32
- 은닉층 개수 : 3개
- 뉴런 개수 : 256 -> 128 -> 64
- 드롭아웃층 : 없음
- MSE : 57894
