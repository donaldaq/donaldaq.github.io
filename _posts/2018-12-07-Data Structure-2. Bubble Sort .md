---
layout: post
title: Bubble Sort
excerpt: "Sort"
categories: [Data Structure]
comments: true
---

# 버블 정렬
개인정리 및 기억하기 위해서 **버블 정렬** 을 정리합니다. 

## 목차
1. 버블정렬 설명
2. 복잡도
3. 파이썬 코드



### 1.버블정렬 설명
선택정렬(Bubble Sort)은 순서대로 두 쌍의 수를 계속 비교하여 정렬하는 방법입니다. 가장 간단한 방법이지만 비효율적인 정렬 알고리즘입니다. 

![bubble sort bar](https://user-images.githubusercontent.com/26396102/49686150-9fefd900-fb33-11e8-990a-20f8735a3efb.PNG)

두 쌍의 수를 계속 비교하여 정렬하는 방법이므로 간단한 알고리즘이지만 가장 비효율적이라고 할 수 있습니다. 그러므로 이미 정렬이 되어 있는 상태에서는 빠르게 정렬을 할 수 있지만 그렇지 않은 경우에는 효율을 기대하기 어렵습니다. 

전체 과정을 배열로 보여드리겠습니다. 반복적으로 나타는 부분은 생략했습니다. 

![array bubble sort1](https://user-images.githubusercontent.com/26396102/49686192-4c31bf80-fb34-11e8-90b1-ed7a205068b0.PNG)

![array bubble sort2](https://user-images.githubusercontent.com/26396102/49686196-5d7acc00-fb34-11e8-8b0b-3ef7fe7dfd03.PNG)

### 2. 복잡도
버블 정렬은 비교 횟수와 위치변경 횟수에 비례합니다. 
> 반복1: 비교횟수(n-1), 위치변경 최대횟수(n-1)
>
> 반복2: 비교횟수(n-2), 위치변경 최대횟수(n-2)
>
> ...
>
> 반복n-2: 비교횟수(2), 위치변경 최대횟수(2)
>
> 반복n-1: 비교횟수(1), 위치변경 최대횟수(1)

- 최상의 경우
 1. 비교횟수: i번째 원소를 (n-1)번 비교, n(n-1)/2번 실행
 2. 자리교환횟수: 자리교환 없음

- 최악의 경우
 1. 비교횟수: i번째 원소를 (n-1)번 비교, n(n-1)/2번 실행
 2. 자리교환횟수: i번째 원소를 (n-1)번 교환하므로 n(n-1)/2번 실행

계산 복잡도는 **O(n2)** 의 계산 복잡성을 가지고 있습니다.

### 3. 파이썬 코드

```python
 def BubbleSort(inputList): # 배열을 파라미터로 넣어줍니다.
   for passnb in range(len(inputList)-1,0,-1):
     for(i in range(passnb):
       if inputList[i]>inputList[i+1]:
         temp = inputList[i]
         inputList[i] = inputList[i+1]
         inputList[i+1] = temp
 
 inputList = [30, 7, 15, 38, 12]
 BubbleSort(inputList)
 print(inputList)
```





