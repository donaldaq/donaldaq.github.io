---
layout: post
title: Quick Sort
excerpt: "Sort"
categories: [Data Structure]
comments: true
---

# 퀵 정렬
개인정리 및 기억하기 위해서 **퀵 정렬** 을 정리합니다. 
위키피디아, [ratsgo blog](https://ratsgo.github.io/data%20structure&algorithm/2017/09/28/quicksort/)를 참고하였고
그림은 [Visualgo](https://visualgo.net/en/sorting)를 통하여 실행 및 캡처 하였습니다. 
## 목차
1. 퀵정렬 설명
2. 복잡도
3. 파이썬 코드



### 1.퀵 정렬 설명
퀵 정렬(Quick Sort)은 찰스 앤터니 리처드 호어가 개발한 정렬 알고리즘으로 다른 원소와의 비교만으로 정렬을 수행하는 **비교 정렬**에 속함
퀵 정렬은 n개의 데이터를 정렬할 때, 최악의 경우는 **O(n2)**, 평균적으로는 **O(nlogn)**를 수행한다. 
![quck arranged 1](https://user-images.githubusercontent.com/26396102/50559539-c45a6200-0d3b-11e9-9f0a-70de7ed58f64.PNG)

![quck arranged 2](https://user-images.githubusercontent.com/26396102/50559549-d4724180-0d3b-11e9-9967-f84a303996f5.PNG)

정리하자면 
- 리스트들중에 하나의 수를 고르고, 이것을 피벗(Pivot)이라고 한다. 
- 피벗 앞에는 피벗보다 작은 값, 뒤에는 큰 값이 오도록 하여 리스트를 둘로 분할한다. 
- 분할된 두 개의 리스트를 재귀적으로 반복한다.

전체 과정은 아래와 같습니다. 위키피디아에 있는 그림을 가져왔습니다. 

![sorting_quicksort_anim](https://user-images.githubusercontent.com/26396102/50559652-8f024400-0d3c-11e9-9457-e2a460f59d94.gif)

### 2. 복잡도
퀵 정렬의 계산복잡성은 피벗이 어떤 것인지에 따라 달라진다. 

최악의 경우: 피벗의 왼쪽(Lessor)값이 매번 하나인 경우, 높이가 **n** , 각 층의 **n** 개의 요소에 대해 정렬을 수행해야 한다.

> 복잡도: O(n2)

![worst case](https://user-images.githubusercontent.com/26396102/50559859-fa004a80-0d3d-11e9-9aee-808cc2405e4d.PNG)

최상의 경우: 분할 과정이 균형적인 경우 입니다. 계산 트리 높이가 **n** 에서 **log2 n**으로 줄어든다

> 복잡도: O(nlogn)

![best case](https://user-images.githubusercontent.com/26396102/50559862-02f11c00-0d3e-11e9-86b2-b94b545cab90.PNG)

평균적인 케이스의 복잡도는 O(nlogn)이고 피벗값을 고정위치가 아닌 랜덤 선택 or 중앙값을 정할 경우 계산복잡도를 낮추는데 도움됨


### 3. 파이썬 코드

```python
def Quick_sort(ARRAY):
    ARRAY_LENGTH = len(ARRAY)
    if( ARRAY_LENGTH <= 1):
        return ARRAY
    else:
        PIVOT = ARRAY[0]
        GREATER = [ element for element in ARRAY[1:] if element > PIVOT ]
        LESSER = [ element for element in ARRAY[1:] if element <= PIVOT ]
        return quick_sort(LESSER) + [PIVOT] + quick_sort(GREATER)
 
 inputList = [20, 44, 38, 5, 47, 15]
 Quicksort(inputList)
 print(inputList)
```





