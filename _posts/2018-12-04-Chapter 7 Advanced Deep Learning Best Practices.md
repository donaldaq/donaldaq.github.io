---
layout: post
title: Chapter 7 Advanced Deep Learning Best Practices
excerpt: "Part 2 Deep Learning in Practice"
categories: [Deep Learning with Keras]
comments: true
---

# 7장 딥러닝을 위한 고급도구
케라스 창시자에게 배우는 딥러닝 Chapter7를 정리하였습니다.  
 

## 목차
1. Sequential 모델을 넘어서: 케라스의 함수형 API
2. 케라스 콜백과 텐서보드를 사용한 딥러닝 모델 검사와 모니터링
3. 모델의 성능을 최대로 끌어올리기
4. 요약


## 케라스 콜백과 텐서보드를 사용한 딥러닝 모델 검사와 모니터링

### 콜백을 사용하여 모델의 훈련 과정 제어하기
최적의 검증 손실을 얻기 위해 에포크의 최적화를 위하여 지금까지는 에포크 수를 조정하여 처음부터 훈련을 하였으나
더 좋은 처리 방법은 검증 손실이 더 이상 향상되지 않을 때 훈련을 멈추는 것
**케라스** 의 콜백함수를 이용하여 구현이 가능함, 콜백은 모델의 fit()메서드가 호출될 때 전달되는 객체(특정 메서드를 구현한 클래스 객체)

**콜백** 사용하는 몇가지 사례
- 모델 체크포인트 저장: 훈련하는 동안 어떤 지점에서 모델의 현재 가중치를 저장
- 조기 종료(early stopping): 검증 손실이 더 이상 향상되지 않을 때 훈련을 중지
- 훈련하는 동안 하이퍼 파라미터 값을 동적으로 조정: 옵티마이저의 학습률 같은 경우
- 훈련과 검증 지표를 로그에 기록하거나 모델이 학습한 표현이 업데이트될 때마다 시각화

**콜백함수 예**
> keras.callbacks.ModelCheckpoint
> keras.callbacks.EarlyStopping
> keras.callbacks.LearningRateScheduler
> keras.callbacks.CSVLogger

### ModelCheckPoint와 EarlyStopping 콜백
1. EarlyStopping 콜백: 정해진 에포크 동안 모니터링 지표가 향상되지 않을 때 훈련을 중지할 수 있음
2. 일반적으로 EarlyStopping 콜백은 훈련하는 동안 모델을 계속 저장해주는 ModelCheckpoint와 함께 사용

'''python
import keras

 callbacks_list = [
  keras.callbacks.EarlyStopping( # 성능향상이 멈추면 훈련을 중지
  monitor='val_acc',  # 모델의 검증 정확도를 모니터링
  patience=1, # 1 에포크 보다 더 길게(즉 2 에포크 동안) 정확도가 향상되지 않으면 훈련 중지
  ),
  keras.callbacks.ModelCheckpoint( # 에포크마다 현재 가중치를 저장
  filepath='my_model.h5', # 모델 파일의 경로
  monitor='val_loss', # 이 두 매개변수는 val_loss가 좋아지지 않으면 모델 파일을 덮어쓰지
  save_best_only=True, # 않는다는 뜻. 훈련하는 동안 가장 좋은 모델이 저장됨
  )
]
model.compile(optimizer='rmsprop',
  loss='binary_crossentropy',
  metrics=['acc']) # 정확도를 모니터링하므로 모델 지표에 포함되어야 함
  
model.fit(x, y,  # 콜백이 검증 손실과 검증 정확도를 모니터링하기 때문에 
  epochs=10,     # validation_data 매개변수에 검증 데이터를 전달해야 함
  batch_size=32,
  callbacks=callbacks_list,
  validation_data=(x_val, y_val))
'''

### ReduceLROnPlateau 콜백
ReduceLROnPlateau 콜백: 검증 손실이 향상되지 않을 때 학습률을 작게 할 수 있음

'''python
callbacks_list = [
  keras.callbacks.ReduceLROnPlateau(
   monitor='val_loss' #모델의 검증 손실을 모니터링
   factor=0.1, # 콜백이 호출될때 학습률을 10배로 줄임
   patience=10, # 검증 손실이 10 에포크 동안 좋아지지 않으면 콜백이 호출
   )
]

model.fit(x, y,
   epochs=10,  # 콜백이 검증 손실을 모니터링하기 때문에 validation_data 매개변수에 검증 데이터를 전달
   batch_size=32,
   callbacks=callbacks_list,
   validation_data=(x_val, y_val))

'''
 

### 자신만의 콜백 만들기
나만의 콜백은 **keras.callbacks.Callback** 클래스를 상속받아 구현

- on_epoch_begin: 각 에포크가 시작할 때 호출
- on_epoch_end: 각 에포크가 끝날 때 호출
- on_batch_begin: 각 배치 처리가 시작되기 전에 호출
- on_batch_end: 각 배치 처리가 끝난 후에 호출
- on_train_begin: 훈련이 시작될 때 호출
- on_train_end: 훈련이 끝날 때 호출

## 텐서보드 소개: 텐서플로의 시각화 프레임워크

![development loop](https://user-images.githubusercontent.com/26396102/49582978-0f31c580-f99a-11e8-9d8c-278267350b1f.PNG)

위 그림과 같이 
 - 시각화 프레임워크 텐서보드
 - 딥러닝 프레임워크 케라스
 - 하드웨어 시스템

**텐서보드** 의 핵심 목적은 훈련 모델의 내부에서 일어나는 모든 것을 시각적으로 모니터링할 수 있도록 돕는 것

**텐서보드 기능**
 - 훈련하는 동안 측정 지표를 시각적으로 모니터링합니다. 
 - 모델 구조를 시각화합니다.
 - 활성화 출력과 그래디언트의 히스토그램을 그립니다. 
 - 3D로 임베딩 표현합니다. 

'''python
callbacks = [
   keras.callbacks.TensorBoard(
   log_dir='my_log_dir', # 로그 파일이 기록될 위치
   histogram_freq=1,     # 1 에포크마다 활성화 출력의 히스토그램을 기록
   embeddings_freq=1,    # 1 에포크마다 임베딩 데이터를 기록
 )
]
history = model.fit(x_train, y_train,
   epochs=20,
   batch_size=128,
   validation_split=0.2,
   callbacks=callbacks)
'''

**측정 지표 모니터링 히스토그램**

![tensorboard monitoring](https://user-images.githubusercontent.com/26396102/49583540-e7436180-f99b-11e8-8c3d-0651a8e268ec.PNG)

**활성화 출력 히스토그램**

![activation histogram](https://user-images.githubusercontent.com/26396102/49583660-3c7f7300-f99c-11e8-9e55-545edc903aa9.PNG)

**반응형 3D 단어 임베딩의 시각화**

![reaction embedding](https://user-images.githubusercontent.com/26396102/49583735-73558900-f99c-11e8-917c-6bc082cda9b7.PNG)

**텐서플로 그래프 시각화**

![tensorflow graph](https://user-images.githubusercontent.com/26396102/49583869-c92a3100-f99c-11e8-9f02-a86f7ef38c30.PNG)

'''python
from keras.utils import plot_model

plot_model(model, to_file='model.png')
'''
그래프를 이미지로 저장할 수도 있다. 

**크기 정보가 포함된 모델 그래프**

![model graph with shape](https://user-images.githubusercontent.com/26396102/49583990-2d4cf500-f99d-11e8-822d-9d1fd4e5cc19.PNG)


## 모델의 성능을 최대로 끌어올리기
최고의 딥러닝 모델을 만들기 위한 방법

### 고급 구조 패턴

잔차 연결 외 2가지의 디자인 패턴
- 정규화
- 깊이별 분리 합성곱

**배치 정규화**
**정규화(normalization)** 는 머신 러닝 모델에 주입되는 샘플들을 균일하게 만드는 광범위한 방법
데이터에서 평균을 빼서 데이터를 원점에 맞추고 표준 편차로 나누어 데이터의 분산을 1로 만듭니다. 

[ **normalized_data = (data - np.mean(data, axis=...)) / np.std(data, axis=...** ]

**배치 정규화(batch normalization)** 
 - 훈련하는 동안 평균과 분산이 바뀌더라도 이에 적응하여 데이터를 정규화
 - 훈련 과정에 사용된 배치 데이터의 평균과 분산에 대한 **지수 이동 평균(exponential moving average)** 을 내부에 유지
 - 배치 정규화의 주요 효과는 잔차 연결과 매우 흡사
 - ResNet50, Inception V3, 엑셉션 같은 경우 배치 정규화를 사용함

### 깊이별 분리 합성곱
**깊이별 분리 합성곱(depthwise separable convolution)**Con2D를 대체하면서 더 가볍고, 더 빠른 모델의 성능을 몇 퍼센트 포인트 높일 수 있는 층(separableConv2D)
 - 입력 채널별로 따로따로 공간 방향의 합성곱을 수행
 - 점별 합성곱(1X1 합성곱)을 통해 출력 채널을 합침
 - 공간 특성의 학습과 채널 방향 특성의 학습을 분리하는 효과
 - 입력에서 공간상 위치는 상관관계가 크지만 채널별로는 매우 독립적이라고 가정시 타당
 - 모델 파라미터와 연산이 수를 크게 줄여 주기 때문에 작고 더 빠른 모델을 만듦
 - 합성곱을 통해 더 효율적인 표현으로 학습하기 때문에 적은 데이터로도 더 좋은 표현 학습, 결국 성능이 더 높은 모델 만듦

![deeply convnet](https://user-images.githubusercontent.com/26396102/49584939-4905ca80-f9a0-11e8-8f75-d637429957a4.PNG)

### 하이퍼파라미터 최적화
- 얼마나 많은 층을 쌓아야 할까?
- 층마다 얼마나 많은 유닛이나 필터를 두어야 하나?
- relu활성화 함수를 사용해야 하나? 아니면 다른 함수를 사용해야 하나?
- 어떤 층 뒤에 BatchNormalizaton을 사용해야 하나?
- 드롭아웃은 얼마나 해야 하나? 등등 

하이퍼파라미터(Hyperparameter) 최적화를 위해 고려할 사항이 많음
**!!공식적인 규칙은 없다!!**

전형적인 하이퍼파라미터 최적화 과정
 1. 일련의 하이퍼파라미터를 (자동으로) 선택함
 2. 선택된 하이퍼파라미터로 모델을 만듦
 3. 훈련 데이터에 학습하고 검증 데이터에서 최종 성능을 측정
 4. 다음으로 시도할 하이퍼파라미터를 (자동으로) 선택
 5. 이 과정을 반복
 6. 마지막으로 테스트 데이터에서 성능을 측정

##### 하이퍼파라미터 선택 알고리즘
 1. 베이지안 최적화(bayesian optimization)
 2. 유전 알고리즘(genetic algorithm)
 3. 간단한 랜덤 탐색(random search)

[Link-Hyperopt](https://github.com/hyperopt/hyperopt)
[Link-Hyperas](https://github.com/maxpumperla/hyperas)

### 모델 앙상블
**모델 앙상블(model ensemble)** 가장 좋은 결과를 얻을 수 있는 또 다른 강력한 기법
앙상블은 여러 개 다른 모델의 예측을 합쳐서 더 좋은 예측을 만듦

'''python
 preds_a = model_a.predict(x_val)
 preds_b = model_b.predict(x_val)
 preds_c = model_c.predict(x_val)
 preds_d = model_d.predict(x_val)
 final_preds = 0.5 * preds_a + 0.25 * preds_b + 0.1 * preds_c + 0.15 * preds_d # 각 모델의 가중치를 부여
''' 

앙상블의 핵심은 앙상블의 후보 모델이 얼마나 다양한지가 중요!!
예) 트리 기반 모델(랜덤 포레스트, 그래디언트 부스팅 트리), 심층 신경망 - 앙상블




