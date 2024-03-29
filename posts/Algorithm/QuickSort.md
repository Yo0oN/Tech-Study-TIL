---
created: 2020-07-05
modified: 2020-07-05
tag: [Algorithm, Sort]
title: QuickSort
author: Yo0oN
category: Algorithm
---

## 1. 퀵정렬

퀵정렬은 기준점을 중심으로 기준점보다 작은 수는 왼쪽, 큰 수는 오른쪽으로 나눈 후,<br>
왼쪽과 오른쪽에서도 각각 기준점을 잡고<br>
다시 작은수는 왼쪽, 큰수는 오른쪽으로 보내는 방법을 반복하여 정렬을 해주는 정렬이다.

기준점을 설정하는 방법은 여러가지가 있는데 보통 첫번째, 마지막, 중간을 사용한다.

![01](https://user-images.githubusercontent.com/53729311/180646324-1bbe9434-fed2-4967-a826-9a01d13c2bc5.jpg)

또한 퀵정렬은 같은 수의 위치가 바뀌는 불안정 정렬이다.

<br>

### 1-1. 복잡도

퀵정렬은 기준점으로 잡은 수가 해당 배열의 중간값인 최선의 경우라면<br>
분할수 $$log n$$, 합하는경우 $$n$$으로 $$Ω(n log n)$$이 되지만,<br>
최악의 경우(최소값이나 최대값을 기준으로 잡은 경우)라면 $$O(n^2)$$이 된다.

이를 보완하기 위하여 배열의 처음, 마지막, 중간값을 비교하여<br>
셋 중 가운데값을 기준점으로 잡아주기도 한다.

[시간, 공간복잡도 참고](https://www.bigocheatsheet.com/)

<br>

## 2. 구현하기 - Python

```python
def quickSort(list) :
  # 길이가 1보다 작거나 같으면 그대로 반환
  if len(list) <= 1 :
    return list
  
  # 기준점은 중앙의 값
  pivot = len(list) // 2
  left = []
  right = []
  
  for i in range(0, len(list)) :
    # 기준점이라면 넘어감
    if i == pivot :
      continue
    # 기준점보다 작다면 왼쪽으로
    if list[i] < list[pivot] :
      left.append(list[i])
    # 크거나 같으면 오른쪽으로
    else :
      right.append(list[i])
  
  return quickSort(left) + [list[pivot]] + quickSort(right)
```
