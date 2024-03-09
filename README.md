# ML_team1_Prediction_House_Price

<img width="651" alt="스크린샷 2024-03-09 오후 2 37 05" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/ee2c82d8-63f3-474d-ac91-503d7f9dd762">

-------

## 1. 주제 선정 배경

<img width="646" alt="스크린샷 2024-03-09 오후 2 08 57" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/dd65351b-a3f6-437a-ae86-01c56055aeba">

- 오늘날 서울 대학가 청년층 주거 문제는 사회 문제로 대두되고 있음. 
- 오피스텔 월세, 원룸 월세는 코로나 이후 매우 가파른 상승세를 보이며 학생들이 감당하기 힘든 수준.
- 역전세 등으로 전세사기 문제도 곳곳에서 터지며 학생들은 '집 구하기'에 대하여 두려움이 커짐. 

따라서 본 연구는 '서울특별시 오피스텔 실거래가 분석을 통한 집값 예측'을 주제로 대학생들의 주거 문제에 도움을 제공하고자 한다. 


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

데이터 전처리 과정은 다음과 같다. (연도별 경제 성장률, 전/월세 전환율을 모두 적용하여 물가를 반영함.)

<img width="659" alt="스크린샷 2024-03-09 오후 2 10 51" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/5671da24-d4df-4544-a830-6576b923b4a9">



![그림1](https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/1cb08e39-d631-4786-880a-d74f9824fe9d)
![그림2](https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/743fbfe8-8c8b-4d42-93e3-9ffd77d9da1a)

<img width="659" alt="스크린샷 2024-03-09 오후 2 10 51" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/5671da24-d4df-4544-a830-6576b923b4a9">
<img width="656" alt="스크린샷 2024-03-09 오후 2 11 19" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/400a91e8-4904-47e5-858e-8c1d6f883f16">
<img width="342" alt="스크린샷 2024-03-09 오후 2 11 42" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/f5abbe2b-bef3-43b7-bbe7-dbd7a81d7a6f">
<img width="658" alt="스크린샷 2024-03-09 오후 2 12 22" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/275b3f46-0822-49e2-af76-026f70d06398">
<img width="658" alt="스크린샷 2024-03-09 오후 2 12 39" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/d2ec3063-3f81-4d24-b395-3c466fb2cdf7">
<img width="658" alt="스크린샷 2024-03-09 오후 2 12 45" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/
<img width="651" alt="스크린샷 2024-03-09 오후 2 37 05" src="https://github.com/khuda-5th/ML_team1_Prediction_House_Price/assets/158314564/ee2c82d8-63f3-474d-ac91-503d7f9dd762">
assets/158314564/6e564070-dcc2-4329-848d-d88533eb3fe7">


