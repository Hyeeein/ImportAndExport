# Troubleshooting BigData Utilization Project

### 🥇 삼성 멀티캠퍼스 문제해결 빅데이터 프로젝트 경진대회 최우수상 수상
- 주제: 포스트 코로나 시대에 대응하는 국내 수출입 품목별 경쟁력 예측 (자동차 부품, 반도체)
- 기간: 2022.03.18~2022.04.01
- 참여 인원
  - 김현아, 박혜인: 반도체 및 자동차 부품 수출입 ARIMA, 다중회귀분석 <br>
  - 임승찬(팀장), 조완제 : TSI지수 ARIMA 분석


## 1. 프로젝트 기획 배경 및 목표
* 프로젝트 기획 배경
  - 국내 전통 산업의 견고한 성장
  - ICT 기술 발달에 따라 반도체 및 자동차 부품 수요 증가

* 프로젝트 목표
  - 포스트 코로나 시대의 자동차부품, 반도체 품목 **수출입 예측 모델 수립**
  - 한국과 주요국 간의 품목별 **수출경쟁력 비교 분석 및 예측**
  - 변화하느 수출입에 따른 품목별 공급 및 수요 시사점에 대한 **인사이트 도출**


## 2. 주제 설명 및 품목 선정 과정
### (1) 주제에서 말하는 **경쟁력**의 의미

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/03d8fd43-a2c2-4e8b-87b5-25ce490df076)

### (2) 분석대상을 **자동차부품, 반도체 부품**으로 선정한 이유

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/611089ed-bfc3-4b36-a858-de7267b9feb0)

- 한국의 10대 수출품목 중 연간 수출액이 가장 높은 **반도체**와 수출액 5위인 **자동차부품** 품목을 선택하였음
- 코로나 19 백신 이후, **온택트 트렌드**가 보편화 되어 반도체 산업이 더욱 증가할 것으로 추측
- 반면, 자동차 부품 산업의 수출 급감, 부품 수급 차질로 인한 완성차 **생산공잔의 가동중단**과 **글로벌 완성차 판매 감소**
- 코로나 19로 인해 생산과 판매량이 증가하기도 하고 감소하기도 했는데, 코로나 종식 이후인 2022년에는 어떤 결과를 가져올지 예측하기 위해 위와 같은 프로젝트를 진행

### (3) 품목별 피처 변수 선정 과정

* 품목별 수출입 경쟁력에 영향을 줄 수 있는 요인 변수 추출 과정
* 반도체, 자동차부품 산업에 대한 자료 조사를 바탕으로 총 8개의 특성 추출
* 최종 피처 변수

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/265d7b71-a864-4f9c-a9c8-7998c585e559)


## 3. 데이터 전처리
### (1) 사용 데이터 목록

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/cabe3c45-1862-479c-804f-d54537e7ad27)

### (2) 데이터 전처리

* 다중회귀분석, ARIMA 시계열 분석을 위한 데이터셋 구성
  - [자동차부품 코드 ⭐ Hyein's Part !!](https://github.com/Hyeeein/ImportAndExport/blob/master/Data%20Preprocessing/Automotive%20Parts_Datasets.ipynb)
  - [반도체 코드](https://github.com/Hyeeein/ImportAndExport/blob/master/Data%20Preprocessing/Semiconductor_Datasets.ipynb)
  - 코드 실행 후, 전처리된 데이터셋 파일 새로 저장하여 사용

* 자동차부품, 반도체 산업의 TSI, RCA 지수 계산식을 사용하여 새로운 값 생성

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/4015d7c3-5fb4-4940-b85a-b31e5799d24d)
![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/fce87d0c-eed1-4b91-ae32-2abfbc84a2c6)


## 4. 다중회귀분석
선형회귀 분석 전, 모델 가정인 정규성과 등분산성을 확인하고 유의하지 않은 피처는 삭제 (p-value 사용)

그리고 실제 2022년 값과 모델 출력 값이 얼마나 유사한지 scatter plot으로 확인하고 <br>
해당 모델을 MSE, RMSE, MAE, R2_Score 값을 확인하여 성능 평가 진행 → 실제 데이터를 대입해 예측 결과 확인

### (1) 자동차부품 ⭐ Hyein's Part !!

#### ▷ 선형 회귀모델 가정 확인 (정규성, 등분산성 검정) *사진 순서는 수출액, 수입액 순서임. 이하 동일*

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/ce6f0c63-f8db-4ab0-989c-27b45efb5e7e)
![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/3209b5f2-d5db-4990-a746-522fb5e1a998)

수출액, 수입액 모두 정규성과 등분산성을 만족하므로 OLS 모델 구축에 활용 가능

#### ▷ OLS Regression으로 유의성 검정 후 피처변수 제거, 모델 선언 및 학습

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/5fadce2c-ddbc-46fe-9c99-d5fa628cd975)

수출액의 경우, p-value 값이 0.05가 넘지 않는 피처 변수로 **환율, 기준금리, 고용률** 제거 <br>

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/8073fd89-a2a2-4c96-9985-f50dc733c989)

수입액의 경우, p-value 값이 0.05가 넘지 않는 피처 변수로 **국제유가, SCFI, 고용률** 제거 <br>
따라서, 위와 같은 회귀식 도출. 이때 수출입과 수입액 모두 고용률은 유의하지 않은 변수로 선택되어 제거

#### ▷ Scatter Plot을 활용한 미래 반응변수 값 예측

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/1effc0bf-2ec5-4b8a-a3a5-6b36db60ba6d)
![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/a5b07a34-c02f-45d2-9406-91dc3ea4580c)

순서대로 수출액, 수입액에 대한 반응변수 값 예측인데, 두 가지 모두 실제 값과 모델 출력값이 거의 유사함을 알 수 있음

#### ▷ 해당 모델 성능 평가

**<수출액에 관한 해당 모델의 성능 평가 결과>**

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/c0f806e6-93dc-4133-962e-f8a31276249c)

테스트용 데이터셋 성능평가 결과, 결정계수가 81.8%의 정확도를 가지고 있음 <br>
또, 각각 **RMSE가 160,421**이므로, **예측값과 실제값의 차이가 이 수치만큼 차이날 수 있음**을 예상할 수 있음

테스트용 데이터가 아닌, 회귀분석에 사용하지 않은 2022년 1~2월 데이터셋을 사용하여 실제값과 비교한 결과

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/a35e1938-050e-4d5c-90ec-67c8e53ee3f1)

RMSE 값인 160,421와 유사하게 차이난다는 점에서 수출액을 거의 유사하게 예측함을 확인할 수 있음

**<수입액에 관한 해당 모델의 성능 평가 결과>**

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/08729025-63c6-4c5f-93a7-2ff7a2f47e16)

테스트용 데이터셋 성능평가 결과, 결정계수가 74.1%의 정확도를 가지고 있음 <br>
각각 **RMSE가 22,085**이므로, **예측값과 실제값의 차이가 이 수치만큼 차이날 수 있음**을 예상할 수 있음

테스트용 데이터가 아닌, 회귀분석에 사용하지 않은 2022년 1~2월 데이터셋을 사용하여 실제값과 비교한 결과

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/a596fc2e-5fa7-4976-aa2e-9227ba3fca95)

2022년 1~2월 자동차부품 수입액은 예측값과 실제값의 차이가 RMSE 값인 22,085보다는 더 큰 차이가 남 <br>
수출보다는 예측력이 조금 떨어짐을 확인할 수 있음


### (2) 반도체

#### ▷ 선형 회귀모델 가정 확인 (정규성, 등분산성 검정) *사진 순서는 수출액, 수입액 순서임. 이하 동일*

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/c079e4b8-46bf-4df3-b2b2-ec58c51a3bbf)
![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/d24d7080-31e3-4175-9973-b9e23f54b7fc)

수출액, 수입액 모두 정규성과 등분산성을 만족하므로 OLS 모델 구축에 활용 가능

#### ▷ Train, Test 데이터셋 분리

#### ▷ OLS Regression으로 유의성 검정 후 피처변수 제거, 모델 선언 및 학습

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/9250e868-7f59-4e74-82a4-3e217520fee7)
![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/aa998af3-42f8-4b70-a33a-9e20816aee96)

수출액, 수입액 모두 유의성 검정 시 유의한 결과를 나타내어 피처변수 제거 없이 학습 진행

#### ▷ Scatter Plot을 활용한 미래 반응변수 값 예측

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/07ae6c6f-c6f4-44d5-89d8-b85b5fec09e5)
![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/4f1337a9-ee5a-467e-a5d3-184ebb84881c)

순서대로 수출액, 수입액에 대한 반응변수 값 예측인데, 두 가지 모두 실제 값과 모델 출력값이 거의 유사함을 알 수 있음

#### ▷ 해당 모델 성능 평가

**<수출액에 관한 해당 모델의 성능 평가 결과>**

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/d380225f-1592-4a4f-96d6-b21055d97240)

테스트용 데이터셋 성능평가 결과, 결정계수가 79.8%의 정확도를 가지고 있음 <br>
또, 각각 **RMSE가 953,129**이므로, **예측값과 실제값의 차이가 이 수치만큼 차이날 수 있음**을 예상할 수 있음

테스트용 데이터가 아닌, 회귀분석에 사용하지 않은 2022년 1~2월 데이터셋을 사용하여 실제값과 비교한 결과

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/c67deeb3-ec3b-4feb-bae2-68f3b63535ef)

RMSE 값인 953,129와 유사하게 차이난다는 점에서 수출액을 거의 유사하게 예측함을 확인할 수 있음

**<수입액에 관한 해당 모델의 성능 평가 결과>**

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/c5eb213d-32d9-44b6-8e93-7b0e802f9565)

테스트용 데이터셋 성능평가 결과, 결정계수가 77.0%의 정확도를 가지고 있음 <br>
또, 각각 **RMSE가 368,070**이므로, **예측값과 실제값의 차이가 이 수치만큼 차이날 수 있음**을 예상할 수 있음

테스트용 데이터가 아닌, 회귀분석에 사용하지 않은 2022년 1~2월 데이터셋을 사용하여 실제값과 비교한 결과

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/f5971306-1b2d-4380-b008-5ffc05ccf234)

RMSE 값인 368,070과 유사하게 차이난다는 점에서 수입액을 거의 유사하게 예측함을 확인할 수 있음

---

## 5. ARIMA 시계열 모형을 활용한 수출입 경쟁력 예측
* ARIMA 분석 프로세스 및 예측 과정

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/f64adcc1-6913-46fb-a5a2-7d1a68f0f08c)

### (1) 자동차부품 ⭐ Hyein's Part !!

#### ▷ 데이터의 정상성 확인 및 차분

#### ▷ 하이퍼 파라미터 추정 & p-value, AIC 값 확인

#### ▷ ARIMA 모델 학습 후 예측 그래프 시각화

#### ▷ 2022.01~2022.03 수출액, 수입액 예측

### (2) 반도체

#### ▷ 데이터의 정상성 확인 및 차분

#### ▷ 하이퍼 파라미터 추정 & p-value, AIC 값 확인

#### ▷ ARIMA 모델 학습 후 예측 그래프 시각화

#### ▷ 2022.01~2022.03 수출액, 수입액 예측

### (3) TSI 결과 및 예측 분석

#### ▷ 자동차부품

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/00132f6d-5fdf-4338-851e-24b8fdbc73d3)

- 차동장치 및 드라이브축(870850), 부분품(870899), 기타(870829), 클러치(870893), 서스펜션(870880), 운전대(870894) 품목이 수출특화에 가까운 품목이 될 것으로 예측됨
- 완충기(870810)는 수입특화에 가까운 품목으로 예측됨

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/41a62cc2-8707-4b2a-89b9-764837afd472)

- TSI 지수 예측 분석 그래프

#### ▷ 반도체

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/8dc4e8a9-2f52-4e8d-9513-a412a611ae24)

- 메모리 반도체의 경우, 한국이 가장 높은 무역특화지수를 예측하고 있지만 **집적회로반도체 부품**과 **다이오드**는 해외 수입 의존도가 높아진 것으로 예측됨

![image](https://github.com/Hyeeein/ImportAndExport/assets/81239567/db319818-1975-4a6c-a017-87f3add7ed7a)

- TSI 지수 예측 분석 그래프
 
## 6. 결론

* 수출입 금액 예측 모델링 구현에 대한 결론
```
다중회귀분석에서 RMSE 값에 맞춰 수출입 금액의 결과가 예측이 잘 되었음.
하지만, 수출입 금액에 영향을 주는 수많은 피처가 있으므로, 새로운 피처를 찾아 더 나은 예측력을 보일 필요가 있음

ARIMA에서는 2022~2023.3.31까지 예측을 했는데 코로나 19 장기화됨에 따라
수출입 금액의 불확실성 증가된 가운데 정교한 학습과 데이터 확보가 필요함
```

* 경쟁력 예측
```
자동차부품의 TSI 결과, 차동장치 및 드라이브축, 부분품, 기타, 클러치, 서스펜션,
운전대 품목이 수출특화에 가까운 품목이 될 것으로 예측됨. 완충기는 수입특화에 가까운 품목으로 예측.

반도체의 TSI 결과, 메모리 반도체 경우, 한국이 가장 높은 무역특화지수를 예측되고 있지만
집적회로반도체 부품과 다이오드는 해외 수입 의존도가 높아질 것으로 예측됨
```

## 7. 참고자료
- [포트폴리오](https://github.com/Hyeeein/ImportAndExport/blob/master/Documents/%5B%ED%8F%AC%ED%8A%B8%ED%8F%B4%EB%A6%AC%EC%98%A4%5D%20%EA%B5%AD%EB%82%B4%20%EC%88%98%EC%B6%9C%EC%9E%85%20%ED%92%88%EB%AA%A9%EB%B3%84%20%EA%B2%BD%EC%9F%81%EB%A0%A5%20%EC%98%88%EC%B8%A1%20(%EB%B0%98%EB%8F%84%EC%B2%B4%2C%20%EC%9E%90%EB%8F%99%EC%B0%A8%20%EB%B6%80%ED%92%88).pdf)
