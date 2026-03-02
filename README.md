# Stock Prediction

주식 종목을 입력하면 최근 3년 데이터를 기반으로 LSTM 모델을 학습하고, 향후 3개월(90일) 예측값을 생성해 MySQL에 저장하는 프로젝트입니다. Spring Boot 백엔드는 저장된 예측 결과를 조회하는 API를 제공합니다.

**주요 기능**
- 종목 심볼과 epoch 입력 → LSTM 학습 및 예측 생성
- 예측 결과를 MySQL에 저장
- 종목별 예측 결과 조회 API 제공

**프로젝트 구성**
- `prediction/stockprediction.py`: 예측 모델 학습 및 DB 저장
- `back/`: Spring Boot API 서버

**필수 환경**
- Python 3.x
- Java 17
- MySQL

**환경 변수**
루트 `.env`에 DB 접속 정보를 설정합니다.

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=123456
DB_NAME=finance
```

**실행 방법**
1. MySQL에 `finance` DB를 생성합니다.
2. 루트 `.env`를 설정합니다.
3. Python 예측 실행:
```bash
python prediction/stockprediction.py
```
4. 백엔드 실행:
```bash
cd back
./gradlew bootRun
```

**API**
- `GET /api/predictions/symbol/{stockSymbol}`
  - 특정 종목의 예측 결과 조회
  - 결과가 없으면 404 반환

**DB 참고**
- `prediction/stockprediction.py`에서 `stock_predictions` 테이블을 자동 생성합니다.
- `stocks` 테이블은 사전에 존재해야 하며, 예측 결과 저장 시 사용됩니다.
 
