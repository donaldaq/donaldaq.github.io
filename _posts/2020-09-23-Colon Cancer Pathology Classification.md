---
layout: post
title: Colon Cancer Pathology Classification
excerpt: "Projects"
categories: [Projects]
comments: true
---

# Colon Cancer Pathology Classification



I worked and studied Colon Cancer Pathology images deep learning model at Hallym AI center.

This project is ongoing to publish medical journal paper.



#### Deep learning models

- Library: PyTorch
- DenseNet-161
- Inception-ResNet-V2
- Classification Contents: 
  - 6 classes (ADC, TA, TSA, SSA, HP, NC)
  - 2 classes (ADC, Non-ADC)

#### Preprocessing

- Library: OpenCV, imgaug
- All Channels CLAHE
- Resize: 720x480 (All raw image size: 4908x3264)

#### Data augmentations

- Library: imgaug
- Rotation: 60', 90', 120'
- Flip: Horizontal, Vertical
- Data augmentation Flows

![Screenshot from 2020-11-30 10-26-43](https://user-images.githubusercontent.com/26396102/100559615-9fd7dd80-32f6-11eb-8f43-10a49a9b39ac.png)

#### Hyperparameters

- Loss function : Binary Cross-entropy, Categorical Cross-entropy
- Optimizer : adam
- Batch size : 8
- Pretrained model layer freeze: ConvNet as fixed feature extractor
- Learning rate : 0.0001 ~ 1e-7 (learning scheduler: per 10 step X 1/10 rate after previous setting)
- Early Stopping
  - Starting point: 50 epoch 
  - Patience:  50 epoch (validation loss)

![Screenshot from 2020-11-30 10-29-49](https://user-images.githubusercontent.com/26396102/100559729-0230de00-32f7-11eb-92a2-69394455a6f3.png)

#### Results

##### **GradCAM**

![Screenshot from 2020-11-30 10-43-38](https://user-images.githubusercontent.com/26396102/100560382-f2b29480-32f8-11eb-9330-a79d4f26960d.png)

![Screenshot from 2020-11-30 10-45-50](https://user-images.githubusercontent.com/26396102/100560478-41602e80-32f9-11eb-9f82-4462c96c2733.png)

##### **Confusion Matrix**

![Screenshot from 2020-11-30 10-30-51](https://user-images.githubusercontent.com/26396102/100559777-2db3c880-32f7-11eb-914f-e9b1fe81326d.png)



##### **ROC Curve**

- DenseNet-161

![Screenshot from 2020-11-30 10-32-10](https://user-images.githubusercontent.com/26396102/100559866-60f65780-32f7-11eb-875d-7830ce892127.png)

- Inception-ResNet-V2

![Screenshot from 2020-11-30 10-36-19](https://user-images.githubusercontent.com/26396102/101725670-683a1400-3af4-11eb-8c81-13412f6cd002.png)

