---
layout: post
title: Mobile Deep Learning Optimization Process
excerpt: "Python"
categories: [Python]
comments: true
---



## Mobile Deep Learning Optimization Process



### Problems 

- 모바일에서 구동해야 함 



### - Base Architecture Selection 

 보통의 딥러닝 모델은 최고의 성능을 얻기 위해서 만들어지기 때문에 모바일 환경에 적합하지 않을 수 있음.

- 2017년 구글에서 효율적인 연산량을 갖는 딥러닝 모델 Mobilenet을 발표
- 적용 범위: Classification, Segmentation
- 모델 종류: Mobilenet v2, Nasnet-mobile, PNasnet-mobile 등이 있음

> **Object Detection 방법 종류**
>
> - 1 Stage Detector
>   - Single Shot Detector(SSD): RPN을 따로 두지 않고 미리 정의된 Anchor들에 대해서 Object Detection을 함
>   - 장단점: 효율적인 연산량을 갖는다는 장점, 만족할 만한 성능이 나오지 않음.
> - 2 Stage Detector
>   - Faster RCNN: RPN을 따로 두어 Region Proposal을 받고 해당 Proposal 
>   - 장단점: 연산량이 많음, 더 정확한 Object Detection이 가능 
>
> 2가지 방법에 가장 큰 차이점은 RPN(Region Proposal Network)을 따로 두느냐 두지 않느냐로 구분
>
> Facebook AI Research의 Feature Extractor Stage(FPN)라는 모델을 제시
>
> - U-Net구조에서 Feature Extractor Stage를 접목시킨 방법
> - FPN -> SSD적용한 RetinaNet이라는 모델을 제시 - 기존 SSD보다 좋은 성능을 발휘
>
> **Mobilenet FPN Faster RCNN** 이라는 모델이 있음 

### - Float16/UInt8 Inference

딥러닝 연산에서 대부분의 상수는 **32bit float** 자료형을 사용함. 

최근 딥러닝 연산에서는 상수 자료형을 압축, **16bit의 Half Float, 8bit의 Unsigned Integer**로 트레이닝을 시도하여 획기적으로 모델 용량과 연산량을 줄이면서 성능저하를 최대한 막는 방법들이 보고됨 

- 첫번째 방법

> 모델의 32bit float 상수들을 float16으로 변환시켜 학습 
>
> Parameter update시에 Gradient를 32bit로 하고 inference시에는 16bit상수들만 사용하여 성능 저하 없이 학습 가능 및 모델 용량을 절반으로 줄일 수 있는 학습법

- 두번째 방법

> 32bit float 상수들을 8bit의 Unsigned Integer로 변경하여 학습, 모델 상수들을 그룹화하기에 Quantization라고 불릴수 있음
>
> 굉장히 효율적인 연산이 가능함 Mobilenet과 같은 효율적인 구조 모델에서 Quantization 변환시에 성능이 저하됨 

### - Mobile Deep Learning Framework

모바일 딥러닝 환경에서 가장 중요한 건 ARM프로세서 기반 연산 최적화가 관건, 이 부분에 따라서 2~3배 차이가 나기도 함

- Tensorflow Lite
  - 많은 튜토리얼이 존재함 
  - Graph Transformer라는 불필요한 연산들을 손쉽게 최적화하는 Lite Model 변환이 가능함
  - Mobilenet 구조와 SSD object detector는 TF lite graph로 변환가능한 예제들이 많이 존재
  - 8bit 모델로 쉽게 변환이 가능함 
  - Faster RCNN구조에서는 TF lite graph로 변환 후 실행 중에 에러가 발생, TF lite 디버깅 환경이 잘 구축되지 않아서 커스터마이징이 쉽지 않음
- Caffe2
  - 페이스북에서 발표한 딥러닝 프레임워크
  - 모바일 환경 배포 지원
  - protobuffer 형태로 배포하면 플랫폼 의존성이 없음
  - 튜토리얼 예제가 별로 없음 
  - Python API를 지원하지만 완벽한 Python 환경이 아님
  - 디버깅이 쉽지 않음 



### - etc.(Pruning, Architecture Search)

- Neural Network Pruning
- Weight Clustering
- Neural Architecture Search 