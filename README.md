# ML_team1_Prediction_House_Price

<img width="651" alt="스크린샷 2024-03-09 오후 2 37 05" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/ee2c82d8-63f3-474d-ac91-503d7f9dd762">

-------

## 1. 주제 선정 배경

<img width="646" alt="스크린샷 2024-03-09 오후 2 08 57" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/dd65351b-a3f6-437a-ae86-01c56055aeba">

- 오늘날 서울 대학가 청년층 주거 문제는 사회 문제로 대두되고 있음. 
- 오피스텔 월세, 원룸 월세는 코로나 이후 매우 가파른 상승세를 보이며 학생들이 감당하기 힘든 수준.
- 역전세 등으로 전세사기 문제도 곳곳에서 터지며 학생들은 '집 구하기'에 대하여 두려움이 커짐. 

따라서 본 연구는 '서울특별시 오피스텔 실거래가 분석을 통한 경희대학교 근처 오피스텔 실거래가 예측'을 주제로 대학생들의 주거 문제에 도움을 제공하고자 한다. 


#### 연구 질문:

한국의 집값이 형성될 때에는 해외와 달리 다양한 요인이 있지 않을까? 중요도도 다르지 않을까?

서울 중심부와의 거리 (위도,경도), 지하철 교통, 평수(전용면적), 건축년도 등의 요인과 오피스텔 실거래가 간의 상관관계를 알아보자

--> 우리와 밀접한 정보인 '경희대학교 주변 오피스텔 거래 값'은 어떻게 변동할까?


<img width="646" alt="스크린샷 2024-03-09 오후 2 09 59" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/31286bf4-9757-44db-a2f1-d14d0554d4cf">

-------


## 2. 데이터 수집 및 전처리


### 데이터 전처리 과정:
- 서울시 전체 오피스텔 실거래가 데이터 -> 서울 오피스텔 실거래가 주소 조인
- 회기 오피스텔 실거래가 데이터 -> 연도별 최종 집값 시계열 변화 데이터를 회기와 서울시 전체를 나눔(훈련 세트 / 테스트 세트)
- 서울 지하철 위치정보
  
연도별 최종 집값 데이터를 조인하여 시계열 변화 데이터를 만듦.

<img width="646" alt="스크린샷 2024-03-09 오후 2 10 23" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/05e637f3-6170-4a14-809b-a239751fd3da">

데이터 전처리 과정 참조 (연도별 경제 성장률, 전/월세 전환율을 모두 적용하여 물가를 반영함.)

<img width="659" alt="스크린샷 2024-03-09 오후 2 10 51" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/5671da24-d4df-4544-a830-6576b923b4a9">


<img width="908" alt="그림3" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/8606f1e0-51b4-49e2-b5ea-192fa6a1d5a1">


### 훈련 / 테스트 세트 구분
- 훈련세트: 서울특별시 중심구 (강남구, 용산구, 송파구)의 집유형 전체 

  -->  집 유형을 오피스텔로 제한하고 구역을 서울특별시 전체로 변경함.

- 테스트 세트: '경희대 근처'를 반경 7km 이내로 설정함. 

-------


## 3. 모델링 및 평가

### 머신러닝 기법 선택

- 다중회귀와 라쏘회귀를 통해 변수별 중요도 파악 및 새로운 변수를 생성.
  
  1. 확률밀도 함수를 통해 도출한 가장 적절한 조건의 경희대 근처 임의의 집 설정.
  
  2.  경희대 외부 집을 훈련한 모델로 경희대 근처 임의의 집의 2019~2023 예상 실거래가 도출.
     
- 집값 데이터는 시간에 따라 기록되는 시계열 데이터이기에 ARIMA 모델을 활용하여 시간에 따른 자기상관 구조를 모델링하고 예측.
  
  3. 경희대 근처 임의의 집의 2024년 실거래가를 2019~2023데이터를 바탕으로 아리마 시계열 분석을 통해 예측.

### 특성분포 확인

<img width="656" alt="스크린샷 2024-03-09 오후 2 11 19" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/400a91e8-4904-47e5-858e-8c1d6f883f16">

실거래가 형성요인은 전용면적, 월세금, 층, 건축연도, X, Y 였음. 

모델의 테스트 결과 값은 좋았음. 그러나 정규분포를 가지는 난수를 생성하여 새로운 집값 데이터를 모델에 넣었더니 결과는 (-0.64)

주어진 데이터 프레임을 실거래가에 따라 정렬하고 모든 속성에 대해 MIN-MAX스케일링 후 히트맵으로 시각화해보니, 다른 요인들은 선형성이 없고 오직 평수만 실거래가에 영향을 미친다는 사실을 발견함. 


문제점: 

1. 5개년의 경제성장률을 각각 반영한 집값임. 다른 특성들은 변하지 않았음. 
2. 데이터 수가 2019-2023으로 5가지만 존재하므로 아리마 모델을 활용하기엔 한계 존재.

해결:

1. 2024 경희대 인근 오피스텔 실거래가를 예측하는 것이 아닌, 대상을 서울특별시로 확장. 
2. 자신이 원하는 조건을 만족하는 매물의 2024년 가격을 예측하는 툴을 제작해 거래시 도움 제공을 목표로 잡음.

<img width="658" alt="스크린샷 2024-03-09 오후 2 12 22" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/275b3f46-0822-49e2-af76-026f70d06398">

### 머신러닝 재적용 과정
1. 확률밀도함수 바탕으로 특성 생성: 서울특별시 집값 결정요인들의 분포를 확률밀도함수로 표현함.
2. 라쏘회귀와 XGBOOST: GRIDSEARCH / 랜덤서치를 활용해 모델의 하이퍼파라미터를 튜닝. 이를 이용해 모델을 초기화, 조정된 XGBOOST 모델의 성능을 평가함.
3. 최종모델 적용: 자신이 원하는 조건의 '면적/층/년도/위치(X,Y)'를 입력한 뒤 2024 집값을 예측함.

<img width="658" alt="스크린샷 2024-03-09 오후 2 12 39" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/d2ec3063-3f81-4d24-b395-3c466fb2cdf7">


-------


## 4. 결과해석

실거래가 예측모델을 활용해보니 실제 2024년 실거래가와 최대 약 2천만원~3천만원 가량 차이가 있었고 대부분 거의 근사함. 
<img width="658" alt="스크린샷 2024-03-09 오후 2 12 45" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/6e564070-dcc2-4329-848d-d88533eb3fe7">

### 연구 한계점
1. 상권, 교통, 학군, 여가요소(녹지, 수계)등 인문적 요인은 분석하기 어려움.
2. 시계열 데이터를 분석하기 위해서는 주기가 짧고 방대한 양의 데이터가 필요함.

### 개선 방향 
- 제작한 모델의 활용성을 높이기 위해 부동산 매매 정보 등을 포함하는 것이 필요함.
- 예측의 정확도를 높이기 위하여 집값을 KNN모델을 활용하여 상위 그룹 (3~20개) 으로 분류하여 각 연도별로 학습이 필요함.

### 추가 연구
- 단순 상위 10% 기준 분류 모델의 Accuracy가 약 0.89로 가장 적절하여 웹 구현에 활용하였음.
- 모델과 더불어 매매자 본인의 요구를 더할 수 있도록 예측 그룹을 제시함.
  
![그림1](https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/1cb08e39-d631-4786-880a-d74f9824fe9d)
![그림2](https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/743fbfe8-8c8b-4d42-93e3-9ffd77d9da1a)

