---
layout: post
title: The Way of Data Analysis
excerpt: "Knowhow of Data Analysis"
categories: [Kaggle]
comments: true
---

## Participation of Kaggle Competition Week 1
House Prices : Advansed Regression Techniques를 참가하기 위하여 전처리 부분 학습을 위하여 
먼저 캐글 참여 리뷰를 정리하여 보았습니다. 
Naver D2에서 발표한 카카오 김일두님에 내용입니다. 

# Kaggle
전세계의 머신러닝 데이터가 모이고 전세계의 머신러닝 개발자가 모이는 곳
참가하신 김일두님은 두개의 competition을 참가하였다고 하였습니다. 

* Google Tensorflow Speech Recognition Challenge - Speech Classification
* 2018 Data Science Bowl - Image Segmentation

## 머신러닝을 위한 기본 플로우
1. 문제정의(Problem)
2. 아이디어(Idea)
3. 실험(Experiments)
4. 결과분석(Evaluation)


## Tensorflow Speech Recognition Challenge
### 문제 내용
1초 내외의 짧은 음성 사운드를 12개의 클래스로 구분하라 

- 목표
**짧은 명령어를 이해**하는 단순하고 효과적인 모델을 구현.

- 학습데이터
1초 내외의 음성 명령어 65,000개
12개의 클래스: yes/no/up/down/... **Silience/Unknown**

- 평가
150,000개의 레이블되지 않은 사운드 파일을 분류해서 제출.
Multi-class Accuracy 문제

> 여기서 문제는 Silience나 Unknown처럼 레이블이 되어있지 않거나 Classifier를 통할 수 없는 사운드가 문제라고 합니다. 
> 지금 저 같은 경우도 계기판 이미지 학습을 진행하면서 가장 고민되는 문제는 구별하고 싶은 모델이외의 이미지를 어떻게 처리해야하나가 가장 큰 문제입니다. 
> e.g.) 잘못보낸 계기판과 다른 사진, 비대상 모델 계기판 등등

- DashBoard
 1. Training/Validation Set에서 틀린 데이터 체크
 2. Test Set에서 Score가 낮은 데이터 체크
 3. Clustering을 통해 Train/Valid/Test Set에 대한 이해
 4. 이전 Prediction 결과와 Difference 모아보기

### Idea
김일두님 같은 경우에는 아주 단순한 형태의 베이스라인 모델을 구축하여 빠르게 문제사항을 파악한다고 합니다. 
* 네트워크 인풋 - Spectrogram(2D image)
* 네트워크 구조 - CNN, Lenet-like Architecture, Multi GPU Training

## Tensorflow Speech Recognition Analysis
### Underfitting 문제
**Prediction 결과가 특정 Class로 몰리는 경향이 있음**

1. Data Imbalance문제가 있다. 
2. 12개의 클래스 데이터가 학습 데이터 셋에 서로 다른 양으로 존재
3. 양이 더 많은 클래스로 예측하는 경향이 있다. 

**배치 샘플링 조절**

![1](https://user-images.githubusercontent.com/26396102/46384332-495bbe00-c6f0-11e8-9b2c-81e8e212e4e6.PNG){: alt="4"}

배치 샘플링 조절은 일반적으로 셔플링된 데이터를 끊어서 사용하지 않고 Class i에 대한 선택확률 pi를 거쳐서 Epoch당 비복원추출을 하여 사용하였다고 합니다. 

### Overfiitting 문제
1. **Accuracy: ++트레이닝 > 밸리데이션 >++ 테스트 >> 캐글**
 Training set과 Validation 사이에서 Overfitting이 존재함
 Data Evaluation Metric?
 → Dropout / L2 Regularization 추가
2. **Accuracy: 트레이닝 > 밸리데이션 > ++테스트 >> 캐글++**
 Data Evalution Metric에 문제가 있는 걸까?
 캐글에서 채점은 데이터 중 일부만 사용하는 것과 관련 있을 수도 있음
 → Class 별 Evalution Score 도입, Evaluation Dashboard 개발

오버피팅 문제는 dropout이나 L2 Reqularization을 추가하여 어느정도 해결을 했지만 실제 평가된 수치와 캐글에 제출할 때 수치가 캐글 수치 더 낮게 나와서 클래스 별로 수치를 뽑아서 수치가 빠지는 클래스가 없는지도 확인했다고 합니다.

### HyperParameter Search
- Network Width, Depth?
- Network Initializatioon?
- Dropout Ratio?
- L2 Regularization Decay?

→ 하이퍼파라미터를 최적화하여 성능을 최대로 올렸다고 합니다. 

## Model Architecture Search
기존에 사용하는 LeNet으로 아래와 같은 이유로 최대 성능을 기대할 수 없기 때문에 
- Underfitting: 트레이닝셋에 대해 성능이 더 이상 개선되지 않음
- Overfitting: 테스트셋 등에서 트레이닝셋보다 성능이 많이 떨어짐

### Model Architecture Search
1. 2D CNN Classification 대표적인 모델들로 시작
2. VGG16, Inception v4, Resnet, Densenet, Nasnet ...
[Link-2D NetworkStructure 정리사이트](http://openresearch.ai/image-classification-outline)

여기서 대표적인 모델들의 Evaluation 수치를 클라우드로 돌려서 Search를 했다고 하고 VGG16이 더 좋다고 하더라도
Resnet이나 Inception v$에서 네트워크 튜닝을 해주면 더 성능이 좋아지기 때문에 튜닝을 해줘야 한다고 합니다. 

### Data Augmentation
Over/Underfitting 문제 해결하기 위하여 Data Augmentation을 합니다. 

**선정기준**
- 트레이닝셋/테스트셋 데이터에 대한 클러스터링을 통한 분석
- 밸리데이션 기준 Hard Example(계속 틀리는 데이터셋)분석

**해결방법**
볼륨 조절, Sound Shitfting, Stretch와 Pitch 조절, 노이즈 추가(White, Brown,...)
그런데 Augmentation Parameter도 최적화가 필요하기 때문에 **Data Augmentation Parameter Search**방법을 통하여 
파라미터 최적화를 했다고 합니다. 

##문제 재정의
1초내외의 음성이 정확도가 90%밖에 안나오는 것에 대한 의문을 가지고 문제를 재정의 했다고 합니다. 

![2](https://user-images.githubusercontent.com/26396102/46385609-ec640600-c6f7-11e8-857b-79a17bcbbbf1.PNG){: alt="4"}

여기서 제일 문제는 레이블이 없는 음성들이 데이터에 존재하는데 이것을 어떻게 처리하느냐가 문제였습니다. 
저도 지금 Image Classification을 하면서 가장 큰문제는 Unknown Unknowns문제였습니다 대상 모델 계기판이 아닌 이미지나 모델을 어떻게 처리하느냐가 문제였는데 제가 하는 프로젝트는 걸러내는게 가장 큰 문제라 이 부분을 해결하는 것에서 조금 벗어났지만 어쨋든 이 부분은 binary clasification이 아닌 부분에서는 항상 고민해야 할 부분이 아닌가라는 생각이 됐습니다. 

**Unknown Unknowns를 Out of Distribution이라고 부른다고 합니다.**

그래서 이 부분을 해결하기 위하여 4개정도의 논문을 보고 분석을 하여 적용하고 결과를 확인했다고 합니다 

![3](https://user-images.githubusercontent.com/26396102/46385967-cccddd00-c6f9-11e8-960d-ed853977fccc.PNG){: alt="4"}

첫번째는 GAN방식을 사용하여 Out of Distribution을 만들어서 label을 만드는 내용이라고 하고 speech쪽 내용이 없어서 시도를 해보지 못했고
두번재는 Unknown Unknowns를 트레이닝 반복으로 레이블을 만들어줬다고 하는데 그것도 성능이 개선되지 않았다고 합니다. 

![4](https://user-images.githubusercontent.com/26396102/46386106-7c0ab400-c6fa-11e8-9d27-eb16da691064.PNG){: alt="4"}
세번째 Association은 관계가 있을 만한것들을 정의하고 학습 반복을 통하여 관계가 있을 만한 데이터가 계속 관계있는 레이블로 가도록 강제하는 방법이라고 하는데 Loss 함수를 강제하면 된다고 합니다.
네번째 방법이 가장 개선이 되었다고 하는데 Unlabel데이터 전체를 Unknown으로 넣어서 했다고 합니다. 사실 이 방법과 비슷한 방법을 해봤을 때 이미지에서도 어느정도 결과가 있었는데 김일두님이 하신 방법보다는 좀더 심플하게 해서 정확히 같은 방법이라고는 어려울 것 같습니다. 

## Tips for Practice
모든 것을 자동화한다. 
1. MultiGPU: 실험 가속화: 다양한 실험을 위해서 필수 자원 효율화
2. HyperParameter Search: HyperOpt / GPU Cloud를 이용한 하이퍼파라미터 자동 최적화
3. AutoML: 네트워크 아키텍처 자동 최적화

###HyperParameter Search 
딥러닝에 가장 문제는 중간과정을 알 수 없기 때문에 뭘 잘못해서 뭘 잘못 설정해서 성능이 안나오는지가 확인이 어렵습니다. 

* Neural Network HyperParameter Search
1. 일반적으로 사용되는 방법: Hand Tuning
 - 순차적으로 수행되기 때문에 절차가 오래 걸림.
 - 사람이 수행하기 때문에 고정된 절차를 따르는 것은 아님
2. HyperParameter Search
 - Grid Search
 - Random Search
 - Bayesian Search
 - Tree-structured Parzen Estimators
 같은 방법을 사용하여 Hyperparameter Search를 할 수 있는데 Scipy같은데서 구현이 되어 있기때문에 가져다가 붙여서 쓰면 된다고 합니다. 
3. HyperOpt: Opensource Optimizer : Tree-structured Parzen Estimators 기반
김일두님은 이 방법을 가장 추천한다고 하셨는데 Hyperparmeter를 seed로 GPU에 뿌리고 Next Search에 어떤게 필요한지 범위를 줄여나가는 방법이라고 합니다. 

### AutoML
Network Structure를 자동화
** Efficient Neural Architecture Search via Parameter Sharing**이라는 논문 방법으로 
최초 네트워크를 만들고 그 안에 Network 셀을 Reinforcement Learning을 통하여 최적 네트워크 아키텍처를 만드는 방법이라고 합니다. 
![5](https://user-images.githubusercontent.com/26396102/46386764-449e0680-c6fe-11e8-813e-e29949198a68.PNG){: alt="4"}

## 정리
1. 문제정의(Problem)
**좋은 Evaluation Metric을 명확하게 정의**: 
 * 실험 결과를 정확하게 판단할 수 있는지 검증 
 * Human-Friendly한 형태로 출력해서 검증 절차가 손쉬워야 함
 * 실험 결과가 Submit 결과를 예측할 수 있어야 함
2. 아이디어(Idea)
**무작위로 생각나는 방식을 시도하는 것은 운에 맡기는 일**
 * 모델의 문제를 해결할 근거를 가지고 실험을 설계
 Overfitting: Dropout, Regularization, Augmenttation, Normalization
 Underfitting: Network Width/Depth, HyperParams
   1. Make the training error small
   2. Make the gap between training and test error small
3. 실험(Experiments)
 * MultiGPU Training
4. 결과분석(Evaluation)
 * 다양한 실험은 Parallel하게 좋은 Search 방법으로 
   1. 순차적으로 사람이 튜닝하는 방식은 너무 오래걸리고
   2. 최적의 파라미터를 보장하기 어려움
   3. HypterOpt, Random Search


> * 문제정의-실험-분석의 사이클: 해결해야하는 주요한 문제를 정의하고 과학적인 실험/분석으로 해결
> * 재정의된 문제가 해결하고자하는 문제를 정확하게 정의
> * **Overfitting/Underfitting의 관점에서 실험 설계**
> * 네트워크 구조에 대한 이해
> * 반복적인 **이터레이션**으로 성능 개선
> * 추가적인 **Research**로 한계 넘어서는 방법에 대한 탐색



