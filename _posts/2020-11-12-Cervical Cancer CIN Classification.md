---
layout: post
title: Cervical Cancer CIN Pathology Classification
excerpt: "Projects"
categories: [Projects]
comments: true
---

# Cervical Cancer CIN Pathology Classification



I worked and studied Cervical Cancer CIN Pathology images deep learning model at Hallym AI center.

This project is ongoing to publish medical journal paper.



#### Deep learning models

- Library: PyTorch
- DenseNet-161
- Inception-ResNet-V2
- Classification Contents: 
  - 4 classes (CIN3, CIN2, CIN1, Non-neoplasm)
  - 2 classes (CIN, Non-neoplasm)

#### Preprocessing

- Library: OpenCV, imgaug
- All Channels CLAHE
- Resize: 800x600 (Almost raw image size: 2560x1920)

#### Data augmentations

- Library: imgaug
- Rotation: 90'
- Flip: Horizontal, Vertical
- Data augmentation Flows

![Screenshot from 2020-11-30 11-07-00](https://user-images.githubusercontent.com/26396102/100561433-3f4b9f00-32fc-11eb-8a73-95a60054fcf2.png)



#### Hyperparameters

- Loss function : Binary Cross-entropy, Categorical Cross-entropy
- Optimizer : adam
- Batch size : 16
- Pretrained model layer freeze: ConvNet as fixed feature extractor
- Learning rate : 0.0001 ~ 1e-7 (learning scheduler: per 10 step X 1/10 rate after previous setting)
- Early Stopping
  - Starting point: 50 epoch 
  - Patience:  50 epoch (validation loss)

![Screenshot from 2020-11-30 11-20-41](https://user-images.githubusercontent.com/26396102/100562166-2e9c2880-32fe-11eb-98cb-00152e3437eb.png)



#### Results

##### **GradCAM**

![Screenshot from 2020-11-30 11-24-39](https://user-images.githubusercontent.com/26396102/100562327-b4b86f00-32fe-11eb-85e4-3b8fc176ddec.png)

##### **Confusion Matrix**

![Screenshot from 2020-11-30 11-26-10](https://user-images.githubusercontent.com/26396102/100562374-e5000d80-32fe-11eb-8254-25ca3afa92ad.png)



##### **ROC Curve**

- DenseNet-161

![Screenshot from 2020-11-30 11-27-12](https://user-images.githubusercontent.com/26396102/100562409-052fcc80-32ff-11eb-8ecc-4d48d5c11340.png)



- Inception-ResNet-V2

![Screenshot from 2020-11-30 11-27-53](https://user-images.githubusercontent.com/26396102/100562440-1d075080-32ff-11eb-9929-df796963e4cc.png)



