---
layout: post
title: Normalization, Standardization, Regularization
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