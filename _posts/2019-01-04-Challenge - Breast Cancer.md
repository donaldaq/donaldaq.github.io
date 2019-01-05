---
layout: post
title: What is Breast Cancer
excerpt: "Challenge"
categories: [Challenge]
comments: true
---

# Breast Cancer(유방암)
서울아산병원 챌린지를 위하여 이미지 학습 관점에서 유방암에 대해 정리하였습니다.  
위키피디아, [CAMELYON17](https://camelyon17.grand-challenge.org/Background/)를 참고하였고
한글자료는 [서울아산병원](http://breast.amc.seoul.kr/asan/depts/breast/K/content.do?menuId=4494) 참고 하였습니다. 
## 목차
1. 유방암이란?
2. 유방암 판단 단계
3. 디지털 병리학



### 1.유방암이란?
유방암은 모든 암 중에서 가장 연구가 많이 된 편임에도 환경적 요인과 유전적 요인 두 가지에 의해 발생한다는 명확하지 않은 지식만이 있으며, 아직 유방암 발생의 원인에 관해서는 아직 확립된 정설은 없다. 다만 여러 연구 결과를 통해 몇 가지 요인들이 높은 상관관계를 보이고 있고 그 중 여성 호르몬인 에스트로겐이 발암과정에 중요한 역할 [위키피디아](https://ko.wikipedia.org/wiki/%EC%9C%A0%EB%B0%A9%EC%95%94)

유방암 조기발견
- 유방 자가 검진 방법
- 유방 정기진찰 방법
- **유방사진촬영 방법**

> 보통 사람이 손으로 만져지면 1cm정도라고 할 수 잇고 이렇게 되기까지는 4~7년 걸림
> 유방사진 촬영을 하지 않으면 미세한 유방암을 알기 힘듬
> 만져지지 않는 유방암(occult cancer)라고 하며
> **사진상에 작은 덩어리가 보이거나, 유방조직이 변형되어있거나, 조개 껍질 같은 석회질을 미세하게 갈아서 뿌려놓은 듯한 
> 모앙의 미세한 석회질침착(microcalcification)이 보이기도 하며 혹은 두 가지가 동시에 보이기도 함**

### 2. 유방암 판단단계

#### TNM system: 고형 종양 환자의 암 확산 정도를 분류하는 국제적인 시스템

1. T-Stage: 종양의 크기
2. N-Stage: 암이 림프절로 전이되었는지 여부
3. M-Stage: 종양이 신체의 다른 부위로 전이되었는지 여부

CAMELYON17의 경우는 **N-Stage** 에 포커스를 맞춤

![breast_lymph_node](https://user-images.githubusercontent.com/26396102/50692786-57670500-1078-11e9-986d-a69db048b5bd.png)

### 3. 디지털 병리학
슬라이드 스캐너가 고해상도(픽셀 당 최대 160nm)로 유리 슬라이드를 디지털화하는데 사용되는 의료용 이미징

![resolution_pyramid](https://user-images.githubusercontent.com/26396102/50693677-fb51b000-107a-11e9-9a95-58f61839007e.png)

전체 슬라이드 이미지는 일반적으로 다중 해상도 피라미드 구조로 저장.
이미지 파일에는 원본 이미지의 여러 다운 샘플 버전이 포함되어 있음.
피라미드의 각 이미지는 일련의 타일로 저장되어 이미지의 하위 영역을 빠르게 검색할 수 있음.

일반적인 전체 슬라이드 이미지는 RGB픽셀 형식이 3바이트인 최고 해상도 수준에서 200000 x 100000 픽셀
단일 레벨에서 55.88GB의 비 암축 픽셀 데이터를 의미함

- 고해상도 이미지
![example_high_resolution](https://user-images.githubusercontent.com/26396102/50693869-a1051f00-107b-11e9-9c0c-f5da87331690.png)
- 중해상도 이미지
![example_mid_resolution](https://user-images.githubusercontent.com/26396102/50693873-a1051f00-107b-11e9-8c3e-c86e134ccc0d.png)
- 저해상도 이미지
![example_low_resolution](https://user-images.githubusercontent.com/26396102/50693872-a1051f00-107b-11e9-9f84-cc3e4319b16a.png)

### 4. 다른 팀 자료 정리

1. Harvard Medical School-Massachusetts General Hospital-Center for Clinical Data Science(Team HMS-MGH-CCDS)

![framework](https://user-images.githubusercontent.com/26396102/50715409-71c4d100-10c0-11e9-8301-8e81f715823e.PNG)

- Data preprocessing

![data preprocessing](https://user-images.githubusercontent.com/26396102/50715481-c9633c80-10c0-11e9-9e60-db903df8741d.PNG)

- Data augmentation

> Random flip
> Brightness adjustment
> Color shift in RGB space
> Contrast adjustment

![hard example mining](https://user-images.githubusercontent.com/26396102/50715699-c87eda80-10c1-11e9-8719-3f915cb30c69.PNG)
![patch samples](https://user-images.githubusercontent.com/26396102/50715820-4347f580-10c2-11e9-9164-45fc9b8008ed.PNG)

- Network 

Fully convolutional Resnet-101 with dilated convolution and atrous spatial pyramid pooling

![stride](https://user-images.githubusercontent.com/26396102/50715920-a5a0f600-10c2-11e9-9136-586af009743e.PNG)

![network training](https://user-images.githubusercontent.com/26396102/50715978-dda83900-10c2-11e9-920d-a1002329f12c.PNG)

- Post-processig

![post preprocessing](https://user-images.githubusercontent.com/26396102/50716037-18aa6c80-10c3-11e9-97eb-2093b56febf7.PNG)

- Result

Accouracy of 91% on slide-wise classification
Kappa score of 0.94 on training set

#### Other Team
##### MIL-GPAT

- MIL-GPAT framework
![mil-gpat framework](https://user-images.githubusercontent.com/26396102/50716391-c2d6c400-10c4-11e9-9d30-d341fc99de02.PNG)

- Pre-processig

![mil preprocessing](https://user-images.githubusercontent.com/26396102/50716441-fb769d80-10c4-11e9-9522-813a7bf9aa14.PNG)

- Patch-based classification model

![deep texture network](https://user-images.githubusercontent.com/26396102/50716592-9bccc200-10c5-11e9-9eda-d143ec487e74.PNG)

- Post Process

![mil post process](https://user-images.githubusercontent.com/26396102/50716657-eea67980-10c5-11e9-8dc4-d377e342d48b.PNG)

##### TUe

- TUe Framework
![tue method](https://user-images.githubusercontent.com/26396102/50716749-67a5d100-10c6-11e9-8831-6ebfa1a029ec.PNG)

- Tissue Region Extraction
![tissue region extraction](https://user-images.githubusercontent.com/26396102/50716787-99b73300-10c6-11e9-8acb-42486a62b28c.PNG)

- Data Sampling

![data sampling](https://user-images.githubusercontent.com/26396102/50716870-10ecc700-10c7-11e9-9d55-41582e9c0a25.PNG)

- Train-time Data Augmentation

![train time data augmentation](https://user-images.githubusercontent.com/26396102/50718215-b5273b80-10d0-11e9-8d65-7419125e9776.PNG)

- Test time Color Augmentation
![test time color augmentation](https://user-images.githubusercontent.com/26396102/50718252-06372f80-10d1-11e9-91f8-6ea696ef5436.PNG)
![example of color conversion](https://user-images.githubusercontent.com/26396102/50718261-41396300-10d1-11e9-9799-20ad1920aae2.PNG)

#### 정리
1. 네트워크 구조: VGG, ResNet, GoogLeNet 등 다양하게 사용
2. 데이터 전처리, 후처리가 매우 중요함 
