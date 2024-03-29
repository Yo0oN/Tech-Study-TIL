---
created: 2020-07-06
modified: 2020-07-06
tag: [Algorithm, Sort]
title: MergeSort
author: Yo0oN
category: Algorithm
---

## 1. 병합정렬

병합정렬은 합병정렬이라고도 불리며, 분할정복(큰 문제를 작은 문제로 쪼개서 해결)을 통하여 구현한다.

배열이 있다면, 배열을 반씩 계속해서 쪼갠다.<br>
더이상 작아지지 않을 때까지 쪼갠 후 왼쪽과 오른쪽을 정렬하며 다시 배열에 넣는다.<br>
해당 과정을 반복한다.

시간복잡도는 최악, 최선 모두 O(n log n)으로 앞에서 정리한것들 중 가장 빠르다.

![01](https://user-images.githubusercontent.com/53729311/180646300-4fe1506c-ba85-4b95-9cdd-e7f647ef651d.jpg)

또한 같은 두 수가 변경되지 않는 안정정렬에 속한다.

<br>

## 2. 구현하기 - python

병합정렬은 배열을 나누는 mergeSort에서 합해주는 merge 함수를 호출하여 작성하였다.

```python
def mergeSort(list) :
  if len(list) <= 1 :
    return list
  center = len(list) // 2
  left = mergeSort(list[:center])
  right = mergeSort(list[center:])
  return merge(left, right)

def merge(left, right) :
  leftPoint = 0
  rightPoint = 0
  result = list()

  # 둘다 남아있을 경우
  while leftPoint < len(left) and rightPoint < len(right) :
    # 왼쪽 > 오른쪽이면 오른쪽을 넣고 포인터를 +1
    if left[leftPoint] > right[rightPoint] :
      result.append(right[rightPoint])
      rightPoint += 1
    else : # 왼쪽 < 오른쪽이면 왼쪽을 넣고 포인터를 +1
      result.append(left[leftPoint])
      leftPoint += 1
    
  # 둘다남아있는것이 끝나고 한쪽만 남았을 경우
  while len(right) > rightPoint :
    # 오른쪽만 남았을 경우
    result.append(right[rightPoint])
    rightPoint +=1
    
  while len(left) > leftPoint :
    # 왼쪽 남았을 경우
    result.append(left[leftPoint])
    leftPoint +=1

  return result
```
