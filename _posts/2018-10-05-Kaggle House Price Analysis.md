---
layout: post
title: House Prices in Kaggle
excerpt: "Data Analysis for House Prices"
categories: [Kaggle]
comments: true
---

## House Prices in Kaggle
House Prices : Advansed Regression Techniques를 참가하기 위하여 전처리 부분 자료와 커널을 정리 하였습니다. 
 

## 데이터 분석 및 학습을 위한 Process
1. Data Scanning
2. Summary Statistics
3. Histogram and Scatter Chart
4. Preprocessing
5. Feature Engineering
6. Modeling

기본 프로세스는 위와 같은 순서로 진행합니다. 프로세스는 목적과 내용에 따라 다르게 할 수도 있을 것 같습니다. 


## Data Scanning( 데이터 스캔) & Summary Statistics(요약 통계)
raw data를 그대로 스캐닝을 하여서 어떤 변수가 있는지 데이터 타입은 어떤게 있는지 Categorical, Numerical한 것은 어떤건지 등등을 
확인합니다. 
![1](https://user-images.githubusercontent.com/26396102/46539554-c904ab00-c8f1-11e8-9a98-c585a5fd0c36.PNG){: alt="4"}
![2](https://user-images.githubusercontent.com/26396102/46539683-2698f780-c8f2-11e8-8183-1f08625ed224.PNG){: alt="4"}
> head(): 데이터의 상위 테이블 내용확인
> describe(): 요약 통계 

### 데이터 상관관계 분석
독립변수들 간의 상관관계가 높다면 회귀분석의 결과(Coefficient)를 신뢰하기가 힘들어진다고 합니다. 예를 들면 A 변수와 B 변수의 상관관계가 높은 수준이라면 A의 계수를 오로지 A가 Y에 미치는 영향이라고 보기 어렵다고 합니다. 

![3](https://user-images.githubusercontent.com/26396102/46540279-d02cb880-c8f3-11e8-88a6-27e0f94b4060.PNG){: alt="4"}

두 변수의 상관관계가 높을수록 흰색으로 표현되고 이미지에서 보면 상관관계가 높은 Pair는 4종류가 확인됩니다. 
(YearBuilt-GarageYrBlt, GrLivArea-TotRmsAbvGrd, GarageCars-GarageArea)
특정변수에 대해 Y에 미치는 영향을 정확하게 파악하려면 heatmap을 통하여 상관관계를 확인해야 합니다. 
![4](https://user-images.githubusercontent.com/26396102/46540785-44b42700-c8f5-11e8-8f26-f7e8d846e458.PNG){: alt="4"}
![5](https://user-images.githubusercontent.com/26396102/46540787-4847ae00-c8f5-11e8-9bcd-882477d7be33.PNG){: alt="4"}
![6](https://user-images.githubusercontent.com/26396102/46541150-2f8bc800-c8f6-11e8-932e-d99faa0a05be.PNG){: alt="4"}

## Histogram and Scatter Chart (히스토그램과 스캐터 차트)
- 가장 중요한 SalePrice 데이터 확인
- 데이터의 음수값, 평균보다 훨씬 큰값 등등 데이터 활용 의미 확인
- 실제데이터는 범위를 정할 수 있도록 아웃라이어 처리(winsorization, truncation 활용)

### 히스토그램
![7](https://user-images.githubusercontent.com/26396102/46541605-6f9f7a80-c8f7-11e8-8b21-58633d7aefce.PNG){: alt="4"}

### 스캐터 차트
![8](https://user-images.githubusercontent.com/26396102/46542103-9a3e0300-c8f8-11e8-9d6f-7e89970e691e.PNG){: alt="4"}
![__results___37_0](https://user-images.githubusercontent.com/26396102/46542108-9d38f380-c8f8-11e8-932c-178337c8df20.png)

Y축은 SalePrice이고 독립변수 X축에 맞춰 모든 변수에 대해 스캐터 차트를 표현. 모든 독립변수들에 대해 산점도 확인하면 변수들이 종속변수와 연관관계가 있는지를 한번에 확인할 수 있습니다. 예를 들어 데이터가 수평에 가깝게 뿌려져 있으면 그 변수는 SalePrice와 낮은 관계가 있다라고 판단할 수 있습니다. 데이터의 변수의 종류는 많고 변수간 관계가 복잡할 수 있으므로 정확하고 자세히 볼 필요가 있습니다. 

## Preprocessing(전처리)
Train set과 Test set을 붙이거나 데이터 없는 경우 데이터를 채워주는 처리과정 등을 합니다. 
### Missing Data
- 보편적 Missing Data를 확인
- Missing Data가 무작위적인지 일정 패턴이 있는지 확인한다. 

![9](https://user-images.githubusercontent.com/26396102/46543305-729c6a00-c8fb-11e8-8cd4-f7e26d14ec6a.PNG){: alt="4"}

* Imputation(결측값 대체)
의미에 맞는 널값에 데이터를 채워줍니다. 
![10](https://user-images.githubusercontent.com/26396102/46543683-7086db00-c8fc-11e8-8172-03bffc278b77.PNG){: alt="4"}
![11](https://user-images.githubusercontent.com/26396102/46543861-ef7c1380-c8fc-11e8-8413-01ddd9ec2c36.PNG){: alt="4"}

* Outliar 
 1. Univariate Analysis(일변량 분석)
![12](https://user-images.githubusercontent.com/26396102/46544300-33234d00-c8fe-11e8-9fda-15ff38778301.PNG){: alt="4"}
수치를 보고 낮은 수치 범위가 비슷한 수치거나 0과 멀지 않은 수치를 확인합니다. 
높은 수치 범위는 7이상은 범위밖이거나 0과 먼 수치라는 것을 확인합니다. 
 
 2. Bivariate Analysis(이변량 분석)
![13](https://user-images.githubusercontent.com/26396102/46544721-4f73b980-c8ff-11e8-8d21-c14db8a4f736.PNG){: alt="4"}

## Feature Engineering
다양한 데이터를 결합하거나 Numerical data를 binning(bucketization)등을 통하여 유의미한 데이터로 만듭니다.

- Feature Tuning
비어있는 데이터에 값을 채워줍니다. 
![14](https://user-images.githubusercontent.com/26396102/46565145-9e454180-c947-11e8-8332-20ec585f2eda.PNG){: alt="4"}
![15](https://user-images.githubusercontent.com/26396102/46565224-37745800-c948-11e8-9adf-292c47fb5dc4.PNG){: alt="4"}

- Feature Engineering
화장실에 관련된 데이터를 합쳐서 총합의 화장실 수로 합치는 과정같은 방법으로 Feature Engineering을 합니다. 
![16](https://user-images.githubusercontent.com/26396102/46565301-bff2f880-c948-11e8-8d43-f046e8549ffd.PNG){: alt="4"}
![17](https://user-images.githubusercontent.com/26396102/46565318-0183a380-c949-11e8-8ce8-df9b6d928924.PNG){: alt="4"}
![18](https://user-images.githubusercontent.com/26396102/46565319-06485780-c949-11e8-9f1a-bb5144576596.PNG){: alt="4"}

- Binning 
지역별로 나누어서 Binning을 하여 Categorical하게 바꿔줍니다. 
![19](https://user-images.githubusercontent.com/26396102/46565390-d8174780-c949-11e8-990d-6dcff7f7367b.PNG){: alt="4"}
![20](https://user-images.githubusercontent.com/26396102/46565391-dbaace80-c949-11e8-9929-47ff2c6a4d77.PNG){: alt="4"}

## Modeling

### Preparing data for modeling
데이터를 modeling에서 학습이 잘 되도록 준비해줍니다. 
- Dropping highly correlated variabels
- Removing outliers
- PreProcessing predictor variables
   1. Skewness and normalizing of the numeric predictors
   2. One hot encoding the categorical variables
   3. Removing levels with few or no observation in train or test
- Dealing with skewness of response variable
[Link-Kaggle Kernel](https://www.kaggle.com/erikbruin/house-prices-lasso-xgboost-and-a-detailed-eda)
링크를 보시면 더욱 자세하게 데이터를 처리하는 방법이 있습니다. 

### Selection Model
학습을 위해서 모델을 정하거나 앙상블을 합니다. 
1. Lasso regression model
2. XgBoost model
[Link-Kaggle Kernel](https://www.kaggle.com/erikbruin/house-prices-lasso-xgboost-and-a-detailed-eda)




