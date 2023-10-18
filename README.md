
<h1 align="center"> 
  <br> 
  shopping_project
</h1>

<h3 align="center">
</h3>  
<p align="right">
  <br>
  프로젝트 기반 빅데이터 서비스 개발자 양성 과정 4기  
  <br>이찬녕</br>
</p>   

### Abstract
• 본 보고서는 쇼핑몰 데이터를 이용한 분석을 통해서 기간과 결제 방법 별로 결제 금액을 분석하고, 입점 
기업별 RFM분석을 실시하고 최대 매출 상품에 대한 분석을 시각화를 함으로써 추후 vip 고객기업에 대한 
서비스 제공 및 상품 상품 준비에 있어서 인사이트를 제공하기 위함이다.
<br>
• RFM 분석 : ‘Recency’ 고객이 얼마나 최근에 구매하였는가 에 관련한 최근성, ‘Frequency’ 고객이 얼마나
자주 방문했는지 에 관련한 빈도, ‘Monetary’ 고객이 얼마나 많은 돈을 지불했는지 에 관련한 구매 금액으로 
회사에서 가장 중요한 지표인 최근성, 행동 빈도, 구매 금액 3가지 관점에서 고객의 가치를 분석하는 행위를 
의미한다.
<br>

### Introduction
• 코로나-19에 의해 오프라인 매장의 수요가 급감하고, 온라인 매장의 수요가 급증하면서 고객에 대한 
데이터 및 주문 데이터를 수집하기가 더 쉬워졌다. 그 결과 데이터의 양이 방대해지면서 다양한 분석을 하는 
것이 가능해졌다. 그 예시로 1개의 쇼핑몰의 데이터를 분석해서 다양한 인사이트를 도출함으로써 추후에 
다른 쇼핑몰을 운영할 때, 다양한 상황에 대한 대비와 준비를 할 수 있다.
<br>

### Method
• 데이터가 19년 12월부터 22년 11월까지만 있는 것으로 보아 19년 12월에 오픈해서 22년 11월에 폐업한 
총 36개월 동안만 영업한 쇼핑몰 이라는 가정으로 분석을 진행했다. 
<br>
• 전처리 : 쇼핑몰 실습데이터는 총 12개의 변수에 대해서 218,601개의 관측치로 구성되어 있다. 12개의 
변수 중에서 ‘제작문구 내역’ 컬럼의 결측치는 212,567개이며, ‘할부기간’ 컬럼의 결측치는 216,674개 이다.
두 컬럼에 대해서 대부분의 관측치가 결측치이기 때문에 두 컬럼을 제외해서 data1 으로 저장하고, 두 컬럼이
필요한 분석을 진행한다면 원본 데이터인 data에서 다시 가져와서 분석을 진행하겠다.
<br>

### Result
### [필수 분석] 1. 입점 기업별 RFM 분석 (3그룹) 진행
▪ ‘업체명’ 컬럼을 이용해서 RFM 분석을 진행할 것이기 때문에 ‘업체명’ 컬럼에 결측치가 있는지 확인했다. 1
개의 행에서 결측치를 발견했는데 이 결측치 값의 ‘상품명’ 컬럼 값이 ‘HBE문고리 비닐봉투(주황)-1세트 200
장’ 이었고, 이 상품명을 가진 다른 행들의 ‘업체명’ 컬럼을 찾아본 결과 모두 ‘지니’여서 결측치 또한 ‘지니’로 
채우고 분석을 진행했다.
<br>
▪ RFM 분석에 사용할 ‘업체명’, ‘ 판매금액’, ‘주문일자’ 컬럼만 추출해서 data_rfm 으로 저장했다. 
<br>
▪ 우선 누적 주문금액에 따라서 업체를 분류하기 위해서 업체명 별로 그룹화를 하고 업체명 별로 합계를 
계산해서 grouped_company_sum에 저장했다. 주문을 한 총 89개의 업체 중 누적 합계금액 상위 10%를 
‘vip’로, 상위 50%를 ‘normal’로, 하위 50%의 업체들은 빈 칸으로 해서 grouped_company_sum의 ‘등급’
컬럼으로 저장했다. vip로는 ‘다우기술’, ‘라온웍스’, ‘에이스디포’, ‘오피스퀵’, ‘쥬크박스’, ‘지니’, ‘지니 
태블릿’, ‘지니 태블릿(후불집행)’, ‘천재태블릿’ 이 있고, ‘normal’ 등급의 업체는 총 35개가 있다.
<br>
▪ 최근 구매 여부로 분석을 진행하기 위해서 data_rfm에서 ‘주문일자’의 컬럼 중 yyyy부분인 연도를 
추출했다. 연도 중 2022년을 data_2022로 저장했고, 최근 구매이기 때문에 마지막 해인 2022년의 구매 
데이터 중에서도 마지막 월인 11월을 data_2022_11로 저장했다. 그리고 2022년 하반기에 주문한 
업체들은 data_2022_half1 으로 저장했다.

### [필수 분석] 2. 매출 시각화
▪ 월별, 연도별로 매출을 시각화하기 위해서 data1 에서 ‘판매금액’ 컬럼과 ‘주문일자’ 컬럼만 가져와서 
분석을 진행하겠다. 주문일자는 yyyy-mm-dd HH:MM:SS의 형태로 되어있다. 주문일자 데이터에서 yyyy 
부분과 mm 부분을 추출하여 ‘판매금액’ 컬럼과 같이 각각 data_year, data_month로 저장했다. 각 
데이터를 연도별, 월별로 합계를 계산해서 year_sum 과 month_sum으로 저장했다.
<br>
▪ 연도별 합계를 저장한 year_sum을 시각화한 그래프이다. 2019년,
2020년, 2021년, 2022년의 순서로 막대 그래프를 그렸다. 그래프를
통해서 매출액이 지속적으로 증가하는 것을 확인할 수 있지만, 2019
년의 매출이 비정상적으로 적은 것을 확인할 수 있다. 원본 데이터의 ‘
주문일자’ 컬럼 중 연도가 ‘2019’ 인 관측값의 월 부분을 보면 19년도는
12월부터 데이터가 관측된 것을 알 수 있다. 19년도의 관측값의 갯수도
적고 값 자체도 작기 때문에 따로 분석을 했을 때 유효한 결과를
도출하기는 어렵다 판단되어 2020년 데이터와 통합해서 분석을
진행했다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%801.png" width="800"/>

</p>
<br>
▪ 2019년의 관측값을 2020년과 통합해서 분석한 결과를 시각화 한 그래프에서도 큰 차이를 보이지는 
않았다. 매년 매출액이 증가하고 있는 것을 확인할 수 있었다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%802.png" width="800"/>

</p>
<br>
▪ 다음으로 월별 합계를 저장한 month_sum은 각 연도는
무시하고 모든 연도에 대해서 각 월 별로 합계를 구했다. 모든 월에 대해서 비슷한 매출을 보이지는 않지만 
데이터 분포에 있어서 큰 규칙이 보이지는 않는다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%803.png" width="800"/>

</p>
<br>
<br>

### [필수 분석] 3. 결제 방법에 따른 분석
▪ 결제 방법과 결제 금액의 연관성을 분석하기 위해 판매금액과 결제방법에는 연관성이 없다는 것을 
귀무가설로 세우고, 대립가설은 판매금액과 결제방법에는 연관성이 있다는 것으로 세웠다.
결제 방법과 결제 금액의 연관성을 알아보기 위한 분석이기 때문에 data1의 ‘판매금액’ 컬럼과 ‘결제방법’ 
컬럼을 가져와서 data_how로 저장했다. 판매 금액에는 결측치가 없었지만, 결제 방법에는 총 14개의 
결측치가 있었다. 그리고 혼합된 결제 방법 중 결제 방법을 특정할 수 없는 ‘-’ 과 ‘ + 포’가 있었다. 이번 분석 
주제의 조건인 결제 방법이 한 가지가 아니고 여러 가지가 혼합되어 있는 경우에는 맨 앞의 한 가지만 사용한 
것으로 간주하는 것을 만족하기 위해서 결제 방법이 ‘-’로 되어있는 1361개의 데이터와 ‘ + 포’로 되어있는 2
개의 데이터를 포함해서 14개의 결측치가 있는 행은 삭제했다.
<br>
▪ ‘신용카드’ 가 아니지만 ‘신’으로 시작하는 45871개의 관측값은 결제방법을 신용카드로 바꾸었고, ‘후불’ 이
아니지만 ‘후’로 시작하는 98개의 관측값을 ‘후불’ 로 바꾸었고, ‘적립금’ 이 아니지만 ‘적’으로 시작하는 1354
개의 관측값을 ‘적립금’ 으로 바꾸었고, ‘정기결제’ 가 아니지만 ‘정’ 으로 시작하는 441개의 관측값을 ‘
정기결제’ 로 바꾸었고, 마지막으로 ‘현금간편결제’ 가 아니지만 ‘현’ 으로 시작하는 2066개의 관측값을 ‘
현금간편결제’ 로 바꾸었다.
<br>
▪ 전처리를 끝낸 데이터를 결제방법 별로 묶어서 
grouped_how로 저장한 후에 결제방법 별 판매금액의
합계를 계산해서 grouped_how_sum에 저장했다. 
오른쪽은 grouped_how_sum으로 산점도를 그린 것인데
신용카드로 결제한 주문의 판매금액 합계가 
7,229,661,435원으로 가장 높았다. 그 다음으로는
정기결제로 주문한 판매금액의 합계가 1,490,893,200
으로 두 번째로 높았으며, 다른 결제 방법들 사이에서는 큰
차이를 보이지 않았다. 
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%804.png" width="800"/>

</p>
<br>
▪ 결제 방법별 판매금액의 합계에 대한 연관성을 찾기
위해서 pearson 상관계수 분석을 실시하였다. 결과는 pvalue가 0.66으로 0.05보다 크기 때문에 귀무가설을
채택해서 결제 방법과 판매금액 사이에는 연관성이 없다고 할 수 있다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%805.png" width="800"/>

</p>
<br>
▪ 결제 방법별 합계 말고 판매금액에 대한 평균으로 연관성을
알아보기 위해 grouped_how를 결제 방법별로 판매금액의
평균을 구해서 grouped_how_mean으로 저장했다. 오른쪽의
그래프는 grouped_how_mean의 산점도인데 합계와는
다르게 후불이 1,381,631원으로 매출액이 가장 높았으며, 두
번째로는 합계와 마찬가지로 정기결제가 941,815원이었다. 
하지만 다른 결제방법들에서는 큰 차이를 관측할 수 없었다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%806.png" width="800"/>

</p>
<br>
▪ 결제 방법별 판매금액의 평균에 대한 연관성을 찾기 위해서 
pearson 상관계수 분석을 실시하였다. 결과는 p-value가 
0.11로 0.05보다 크기 때문에 귀무가설을 채택해서 결제
방법과 판매금액의 평균에는 연관성이 없다고 할 수 있다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%807.png" width="800"/>

</p>
<br>
<br>

### [선택 분석] 1. 매출 시각화2 
<br>
▪ 최대 매출 상품 3종류 집계를 위해서 data1 에서 ‘상품명’ 컬럼으로
묶은 뒤에 같은 ‘상품명’ 값에 대해서 ‘판매금액’ 컬럼의 합계를
계산했다. 판매금액 합계를 내림차순으로 정렬해서 상품별 합계를
비교해보았다. 판매금액이 가장 높았던 상품은 ‘[스마트 HBE] 학습
전용 태블릿’ 으로 총 965,844,000원의 판매금액을 보였다. 두
번째로 판매금액이 높았던 상품은 ‘[신세계] 신세계 상품권-4만원권’
으로 총 896,793,600원의 판매금액을 보였으며, 마지막으로 ‘[
지사전용] 스마트 HBE-학습 전용 태블릿’ 가 총 622,908,000원의
판매금액으로 전체 상품 13252개 중에서 상위 3개안에 들었다.
전체 판매금액에 대한 상위 3개 상품의 판매금액의 비율은 약
21.55% 이다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%808.png" width="800"/>

</p>
<br>

▪ 주문 연도에 따른 최대 매출 상품 3종류의 매출 증감을 분석하기 위해서 data1에서 ‘상품명’ 컬럼, ‘
판매금액’ 컬럼, ‘주문일자’ 컬럼을 가져와서 product_year에 저장했다. 각 상품별로 주문 연도에 따른 매출 
증감 분석이기 때문에 판매금액 합계가 가장 큰 ‘[스마트 HBE] 학습 전용 태블릿’ 의 판매금액과 주문일자를 
top3_1에 저장하고, 두 번째로 큰 ‘[신세계] 신세계 상품권-4만원권’의 판매금액과 주문일자를 top3_2에 
저장하고, 마지막으로 세 번째로 큰 ‘[지사전용] 스마트 HBE-학습 전용 태블릿’의 판매금액과 주문일자를 
top3_3에 저장했다. 그리고 각 연도별로 합계를 구한 데이터를 뒤에 _sum을 붙여서 top3_1_sum, 
top3_2_sum, top3_3_sum으로 저장했다.
▪ ‘[스마트 HBE] 학습 전용 태블릿’ 의
경우 주문연도가 2021년과 2022년으로만
나온것으로 보아, 2019년과 2020년에는
판매를 하지 않았던 상품으로 추측된다. 
그리고 2021년에는 194,040,000원,
2022년에는 771,804,000원으로 약 4
배정도 매출이 증가했다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%809.png" width="800"/>

</p>
<br>

▪ ‘[신세계] 신세계 상품권-4만원권’의 경우 주문연도가 2020년, 2021
년, 2022년으로 나왔는데 그 중에서 
2020년의 값이 이상값이라 판단되어
주문일자를 분석해 본 결과, 2020년 11
월부터 판매 데이터가 있는 것으로 보아 
2020년 11월에 출시한 상품으로
추측된다. 그리고 그 이후로 2021년,
2022년 계속해서 매출이 상승하고
있는데 2021년에 254,630,400원에서 
2022년에는 639,897,600원으로 매출이
약 2.5배 상승했다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%8010.png" width="800"/>

</p>
<br>

▪ 마지막으로 ‘[지사전용] 스마트 HBE-학습 전용 태블릿’은
주문연도가 2022년으로만 나왔다.
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%8011.png" width="800"/>

</p>
<br>

### [선택 분석] 2. 연관성 분석
▪ 연관성을 분석하기 위해서 귀무가설은 주문한 달과 판매금액은 상관관계가 없다는 것이고, 대립가설은 
주문한 달과 판매금액은 상관관계가 있다는 것으로 세웠다. 주문한 달과 판매금액의 상관관계를 분석하기 
위해서 data1의 ‘주문일자’ 컬럼에서 mm부분만 추출해서 data1의 ‘판매금액’ 컬럼과 병합해서 
data_month로 저장했다. 월 별로 합계를 구한 뒤 월과 합계액의 연관성을 분석하기 위해 pearson 상관계수
분석을 실시했다. 결과는 p-value가 0.43으로 0.05보다 크기 때문에 귀무가설을 채택해서 주문한 달과 
판매금액은 상관관계가 없다고 할 수 있는 것으로 나왔다. 
<p align="center">
  <img src="https://github.com/ChanNyoungLee/shopping_project/blob/master/%EC%9D%B4%EB%AF%B8%EC%A7%80/%EC%9D%B4%EB%AF%B8%EC%A7%8012.png" width="800"/>

</p>
<br>
<br>

### 개선사항
• 필수분석 1 에서 판매금액의 합계로 업체를 구분할 때 업체명 중 ‘지니’, ‘지니태블릿’, ‘지니태블릿(후불형)’
등 같은 업체일 가능성이 있는 업체명들이 중복되어서 보이는 것을 보아 전처리 작업을 할 때 같은 업체로 
묶어서 분석을 진행했다면, ‘VIP’ 등급으로 다른 업체들이 들어갔을 것이다. 그리고 선택분석 1에서 최대 
매출 상품 3종류를 집계할 때에도 ‘[스마트 HBE] 학습 전용 태블릿’과 ‘[지사전용] 스마트 HVE- 학습 전용 
태블릿’ 과 같이 비슷한 이름의 제품들을 하나로 묶어서 분석을 진행했다면 더 유용한 인사이트를 도출할 수 
있었을 것이다.
