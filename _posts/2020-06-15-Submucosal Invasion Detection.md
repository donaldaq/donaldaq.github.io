---
layout: post
title: Submucosal Invasion Detection
excerpt: "Projects"
categories: [Projects]
comments: true
---

# Submucosal Invasion Detection



I worked and studied Submucosal classification deep learning model at Hallym AI center



#### This project published journal paper

----------------

![journal_title](https://user-images.githubusercontent.com/26396102/100528125-85313600-321c-11eb-8aaf-8e2ca2d7a43e.PNG)



#### Deep learning models

- Library: PyTorch
- DenseNet-161
- Inception-ResNet-V2

#### Preprocessing

- Library: OpenCV, imgaug
- All Channels CLAHE
- Resize: 480x480 (Almost raw image size: 640x480)

#### Data augmentations

- Library: imgaug

- Rotation: 90'
- Flip: Horizontal, Vertical
- Data augmentation Flows

![submucosal augmentation flows](https://user-images.githubusercontent.com/26396102/100528423-1eae1700-3220-11eb-9b0a-af1ef08c4629.PNG)



#### Hyperparameters

- Loss function : Binary Cross-entropy
- Optimizer : adam
- Batch size : 16
- Pretrained model layer freeze: ConvNet as fixed feature extractor
- Learning rate : 0.0001 ~ 1e-7 (learning scheduler: per 10 step X 1/10 rate after previous setting)
- Early Stopping
  - Starting point: 50 epoch 
  - Patience:  50 epoch (validation loss)



#### Results

- **GradCAM**

![GradCAM](https://user-images.githubusercontent.com/26396102/100528288-98dd9c00-321e-11eb-85fe-1081a2a01c1e.png)



- **Confusion Matrix**

![confusion_matrix_densenet](https://user-images.githubusercontent.com/26396102/100528303-c62a4a00-321e-11eb-9ac8-01d8d2d37f66.PNG)



- **AUC score, Optimal Threshold, ROC Curve**

![ROC_curve_for_Submucosal](https://user-images.githubusercontent.com/26396102/100528337-20c3a600-321f-11eb-87c6-fdbeb3979ee7.PNG)

