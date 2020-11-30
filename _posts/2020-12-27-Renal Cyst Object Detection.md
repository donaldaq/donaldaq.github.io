---
layout: post
title: Renal Cyst object detection
excerpt: "Projects"
categories: [Projects]
comments: true
---

# Renal Cyst object detection



I worked and studied Renal Cyst CT images object detection deep learning model at Hallym AI center.



#### Deep learning models

- Library: PyTorch, Keras
- Backbone Network: ResNet101
- Object Detection Model: RetinaNet
- Object Detection Contents: 
  - Epoch: 20
  - Per epoch: 5000 steps
  - Batch size: 1

#### Preprocessing and Data Augmentations

- Library: OpenCV, imgaug
- CLAHE
- Rotation: 10'
- Shear: 10%
- Scaling: 10%
- Horizontal flip: 50%
- Elastic Transformation

#### Results

##### **Good Results (mAP:95.2)**

![Screenshot from 2020-11-30 10-59-21](https://user-images.githubusercontent.com/26396102/100561087-28f11380-32fb-11eb-955c-6e16fc16b91c.png)



**Bad Results (mAP:95.2)**

![Screenshot from 2020-11-30 11-00-39](https://user-images.githubusercontent.com/26396102/100561152-550c9480-32fb-11eb-903d-bbbd37da5b88.png)