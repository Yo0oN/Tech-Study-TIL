---
created: 2020-07-04
modified: 2020-07-04
tag: [Algorithm, Sort]
title: SelectionSort
author: Yo0oN
category: Algorithm
---

## 1. 선택정렬

선택정렬은 원소를 넣을 위치는 정해져 있고, 어떤 원소를 넣을지 선택하는 알고리즘이다.

일단 맨 앞, 배열의 0번부터 시작한다.<br>
배열의 값 중 가장 작은값, 최소값과 0번의 자리를 바꾼다.<br>
다음에는 배열의 0번을 제외한 1번부터 위의 과정을 반복한다.

![01](https://user-images.githubusercontent.com/53729311/180646338-d2673db3-5e7e-40b0-bc20-e0d4f55ad603.gif)

알고리즘이 단순하고 하나의 배열 안에서 교환하기 때문에 다른 메모리 공간을 필요하지는 않지만,<br>
시간복잡도를 생각하면 효율적인 알고리즘은 아니다.

그리고 동일한 수가 있을 때 두 수의 위치가 바뀔 수 있는 불안정(Unstable) 정렬이다.

![02](https://user-images.githubusercontent.com/53729311/180646339-93da31d6-72ee-43db-9477-ca8f10aae3dd.jpg)

<br>

## 2. 시간복잡도

선택정렬은 기준점의 뒤에서 최소값을 찾기 위해 계속 탐색을 해야한다.<br>
배열의 길이가 n개라면 처음 순회를 할 때는 (n-1)번 비교를 해야한다.<br>
두번째는 (n-2), 세번째는 (n-3)...<br>

버블정렬과 마찬가지로 선택정렬도 $$O(n^2)$$이다. (최선의 경우도 $$Ω(n^2)$$이다.)

또한, 계속 같은 배열 안에서 정렬이 이루어지기 때문에 공간복잡도는 $$O(n^2)$$이다.

<br>

## 3. 구현하기 - python

```python
def selectionSort(list) :
  for pivot in range(0, len(list) - 1) :
    minIndex = pivot
    for i in range(pivot + 1, len(list)) : # 기준점 다음부터 마지막까지 배열 순회
      if list[minIndex] > list[i] : # 만약 minIndex의 값보다 현재 탐색중인 i의 값이 작다면
        minIndex = i # minIndex의 값을 현재 탐색중인 i로 바꿔준다.
    print(list)
    list[pivot], list[minIndex] = list[minIndex], list[pivot] # 마지막에는 기준점과 가장 작은 값을 바꿔준다.
```
