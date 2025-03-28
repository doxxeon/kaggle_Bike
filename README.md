# 🚲 Bike Sharing Demand - 캐글 회귀 예측 프로젝트

## 📌 개요
본 프로젝트는 **Kaggle**의 [Bike Sharing Demand](https://www.kaggle.com/competitions/bike-sharing-demand) 대회의 데이터를 바탕으로, 기상 및 시간 정보를 활용하여 **자전거 대여 수요(count)를 예측**하는 회귀 모델을 구축하는 데 목적이 있다.

---

## 📂 데이터 설명
- `datetime`: 날짜 + 시간
- `season`: 계절 (1=봄, 2=여름, 3=가을, 4=겨울)
- `holiday`: 휴일 여부
- `workingday`: 평일 여부
- `weather`: 날씨 (1=좋음, 4=최악)
- `temp`: 온도 (섭씨)
- `atemp`: 체감 온도
- `humidity`: 습도
- `windspeed`: 풍속
- `count`: 자전거 대여 수 (Target)

---

## 🛠 전처리 및 특징 엔지니어링
- `datetime` 컬럼에서 `year`, `month`, `day`, `hour`, `weekday` 파생
- 온도 구간화 라벨링 → `temp_label` (cold ~ very hot)
- 풍속 구간화 라벨링 → `wind_label` (low / mid / high)
- 습도 구간화 라벨링 → `humid_label` (low / normal / high)
- 시간 기반 특성 추가:
  - `is_rush_hour`: 평일 출근 시간 (7~9시)
  - `is_return_hour`: 평일 퇴근 시간 (17~19시)
  - `is_weekend_lunch`: 주말 낮시간 (12~16시)
- 범주형 변수들에 대해 One-Hot Encoding 적용

---

## 📈 모델링
- 회귀 모델 적용:
  - Linear Regression, Ridge, Lasso
  - Random Forest, Gradient Boosting
  - XGBoost, LightGBM
- 최종 모델: **LightGBM + XGBoost 앙상블**
- 평가 지표:
  - RMSLE (Root Mean Squared Log Error)
  - RMSE (Root Mean Squared Error)
  - MAE (Mean Absolute Error)

---

## 🧪 교차검증 및 하이퍼파라미터 튜닝
- **GridSearchCV** 기반 LightGBM 하이퍼파라미터 튜닝
- KFold(n=5) 교차검증 적용
- 최종 앙상블: LGBM + XGBoost 예측 평균

---

## 🏁 결과
- 최고 성능 모델: 앙상블 (LGBM + XGBoost)
- Kaggle 제출 점수: **RMSLE 0.38606**

---

## 📁 프로젝트 구조
```
📦bike-sharing-demand
┣ 📄train.csv
┣ 📄test.csv
┣ 📄submission.csv
┣ 📄notebook.ipynb
┗ 📄README.md
```

---

## 🧰 사용 라이브러리
```python
pandas, numpy, seaborn, matplotlib  
scikit-learn, xgboost, lightgbm
