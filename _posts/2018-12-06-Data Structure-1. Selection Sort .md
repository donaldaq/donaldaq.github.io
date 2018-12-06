---
layout: post
title: Selection Sort
excerpt: "Sort"
categories: [Data Structure]
comments: true
---

# 선택 정렬
개인정리 및 기억하기 위해서 **선택 정렬** 을 정리합니다.

## 목차
1. 선택정렬 설명
2. 복잡도
3. 파이썬 코드



### 1.선택정렬 설명
선택정렬(Selection Sort) 전체 배열에서 최소값(최대값)을 찾아서 위치를 변경해주는 방법입니다.
일반적으로 가장 이해하기 쉬운 방법이라고 할 수 있습니다. 

![selection sorting](https://user-images.githubusercontent.com/26396102/49590467-54142700-f9af-11e8-9dff-cb619b6311cf.PNG)

다음 설명과 같이 가장 작은 수나 큰 수를 찾아서 위치를 변경해주는 방식입니다. 

전체 과정을 보여드리기 위해 아래에는 전체 과정을 배열로 보여드리겠습니다.

![array selection](https://user-images.githubusercontent.com/26396102/49590585-989fc280-f9af-11e8-80f1-1b2da92ddfa2.PNG)

### 2. 복잡도

계산 복잡도는 O(n2)의 계산 복잡성을 가지고 있습니다.

### 3. 파이썬 코드

```python
 def SelectSort(inputList): # 배열을 파라미터로 넣어줍니다.
   for fills in range(len(inputList)-1,0,-1):
     locationOfMin = 0
     for(location in range(1,fills+1)):
       if inputList[location]<inputList(locationOfMin):
         locationOfMin = location
     temp = inputList[fills]
     inputList[fills] = inputList[locationOfMin]
     inputList[locationOfMin] = temp
```





