---
layout: post
title: Confused concepts for Deep Learning
excerpt: "Deep Learning"
categories: [Deep Learning]
comments: true
---

## Confused concepts for Deep Learning



### Normalization, Standardization, Regularization

Normalization, Standardization 모두 데이터를 좀더 Compact하게 만들기 위하여 사용

- 값의 범위(Scale)를 축소하는 re-scaling과정을 의미
- 이유: scale의 범위가 너무 크면 노이즈 데이터가 생성되거나 overfitting이 될 가능성이 높음
- 제곱 손실 함수, 절대값 손실함수 특성에서 보면 제곱 손실 함수를 사용할 경우 비정상적으로 커져 노이즈가 많이 생성 
- 활성화 함수(activation function)을 거치는 의미가 사라짐, 값이 너무 커져 쏠림 현상이 발생



1. Normalization: 다양한 방식이 존재, 픽셀 값 범위(0 ~ 255)를 255로 나눠 0~1의 범위로 축소시키는 방식

2. Standardization: 표준화 확률변수를 구하는 방법. Z-Score 구하기라고 할 수 있음
   $$
   \dfrac{x-\gamma}{\theta}
   $$



3. Regularization:  제약을 건다는 것 Complex 혹은 Flexible하게 만든다는 것, 특정 Penalty 값만 더해주거나 빼주어서 모델의 복잡도를 조정해주는 것
   1. 주로 하이퍼 파라미터를 수정하는 방식으로 Regularization을 함
   2. 종류: L1, L2 Regularization, Drop-out 등이 있음 



------------------

### ReLU, Leaky ReLU, Randomized Leaky ReLU



#### ReLU

- 단순하게 0 이하의 값이 들어오면 활성화 값을 0으로 맞추고 그 이상의 값은 그대로 전달하는 방식

- 0~1으로 들어오는 시그모이드(로지스틱)함수, -1~1으로 들어오는 하이퍼볼릭탄젠트 함수와는 달리 자극이 0 이상이면 그대로 전달해주기 때문에, 전파되는 값들이 크고 역전파되는 값들 역시 y=x 미분하면 1이 나오기 때문에 기울기 값이 그대로 전파되어 **학습 속도**가 빠름

  

#### Leaky ReLU

$$
f(x) = max(ax, x)
$$

- 이 수식을 변형시키고 상수 a에 작은 값을 설정함으로써 0 이하의 자극이 들어왔을 때도 활성화 값이 전달됨
- 예를 들어 a가 0.2라고 하면 0 이하의 자극에 0.2를 곱해 전달하고 0보다 큰 자극은 그대로 전달하는 활성화 함수가 됨



#### Randomized Leaky ReLU

- a의 값을 랜덤하게 지정하는 활성화 함