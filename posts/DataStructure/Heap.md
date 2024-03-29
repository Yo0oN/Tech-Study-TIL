---
created: 2020-07-16
modified: 2020-07-16
tags: [DataStructure]
title: Heap
author: Yo0oN
categories: [DataStructure]
---

## 1. Heap

힙은 여러 자료 중 최대, 최소값을 빠르게 찾기 위해 만들어진 완전 이진 트리로, 우선순위 큐를 위하여 만들어졌다.<br>
 (완전 이진 트리는 가지가 두개이며, 노트를 삽입할 때 최하단 왼쪽 노드부터 차례로 삽입해서 한 레벨에 빈칸이 있으면 다음 레벨로 넘어갈 수 없는 트리를 말한다.)<br>

![01](https://user-images.githubusercontent.com/53729311/180646745-60a9c998-2199-4ab9-9e2f-59b8e96473b8.jpg)

힙에는 최대힙과 최소힙이 있는데, 최대힙은 부모노드가 자식노드보다 무조건 크기 때문에,<br>
루트노드에는 항상 해당 배열의 최대값이 온다.<br>
그 반대로 최소힙은 부모노드가 자식노드보다 무조건 작기 때문에, 루트노드에는 최소값이 온다.<br>
하지만, 힙은 최대나 최소의 위치만 정해진 반정렬 상태로, 다른 값을 찾을 때는 소용 없다는 단점도 있다.<br>

또, 힙은 우선순위 큐를 위하여 만들어졌기 때문에,<br>
힙에서 데이터를 삭제한다고 하면 우선순위가 가장 높은 수가 적혀있는 루트노드를 삭제한다.<br>


### 1-1. 힙의 인덱스

힙은 배열을 이용하여 구현하는것이 편한데, 부모와 자식 노드간 인덱스를 보면 규칙이 있다.<br>


![02](https://user-images.githubusercontent.com/53729311/180646747-0d4c7b58-c2e4-4b66-804b-5b0300e9ce29.jpg)

~~~
부모 index = (자식 index) / 2
왼쪽 자식 index = (부모 index) * 2
오른쪽 자식 index = (부모 index) * 2 + 1
~~~

위의 그림에서 보면 루트가 1인 경우 깔끔하게 자식 노드들의 인덱스를 알아낼 수 있다.<br>
그렇기 때문에 배열을 이용하여 힙을 구현하면 인덱스 0번은 사용하지 않고, 1부터 사용한다.


### 1-2. 복잡도

힙은 데이터를 넣고 뺄 때 위치를 조정해주어야 한다.<br>
부모 노드 값을 통하여 자신이 들어갈 자리를 계속 탐색해야 하는데, 완전 이진 트리이므로 완전 이진 트리를 탐색하는 시간과 똑같이 $$log n$$이다.<br>
삭제를 할 때도 루트노드를 삭제한 후 최대값인 노드를 루트로 다시 옮겨야 하는데 해당 과정도 $$log n$$이 된다.

<br>

## 2. 구현하기

아래에서 구현한 힙은 최대힙이다.

```python
class Heap :
  def __init__(self, data) :
    self.heap_array = list()
    self.heap_array.append(None) # 0번은 비워둔다.
    self.heap_array.append(data) # 1번부터 들어온 값을 넣는다.
```

힙에 데이터를 삽입하는 메서드

```python
def insert(self, data) :
  if len(self.heap_array) == 0 : # 만약 데이터가 하나도 없다면 
    self.heap_array.append(None) # 일단 0번에 None 추가
    self.heap_array.append(data) # 1번에 값 추가
    return True # 데이터 넣은 후 True 반환
  self.heap_array.append(data) # 배열에 데이터가 있다면 이어서 추가
  # 그런데 들어간 데이터가 부모노드보다 크다면 부모와 자리를 바꿔줘야 한다.
  inserted_index = len(self.heap_array) - 1 # 현재 데이터가 들어간 인덱스 번호
  # 루트노드의 자리에 가면 중단한다.
  while inserted_index > 1 :
    # 만약 현재 값이 부모 값보다 크다면 자리를 바꿔준다.
    if self.heap_array[inserted_index] > self.heap_array[inserted_index // 2] :
      self.heap_array[inserted_index], self.heap_array[inserted_index // 2] =  self.heap_array[inserted_index // 2],  self.heap_array[inserted_index]
      inserted_index = inserted_index // 2
    else : # 작다면 중단한다.
      break
```

힙에서 데이터를 빼는 메서드

```python
def pop(self) :
  # 힙에 데이터가 없다면 None 반환
  if len(self.heap_array) <= 1 :
    return None
  result = self.heap_array[1] # 힙의 루트값을 반환해준다.
  # 힙의 가장 마지막 값을 루트노드에 넣어준다.
  self.heap_array[1] = self.heap_array[-1]
  del self.heap_array[-1]
  cur_index = 1
  # 자식노드가 있을 때까지 아래의 과정을 반복한다.
  while cur_index * 2 <= len(self.heap_array) - 1 :
    # 양쪽 노드가 다 있는 경우
    if cur_index * 2 + 1 <= len(self.heap_array) - 1 :
      if self.heap_array[cur_index * 2] > self.heap_array[cur_index * 2 + 1] :
        if self.heap_array[cur_index] < self.heap_array[cur_index * 2] :
          # 왼쪽, 현재, 오른쪽 노드 중 왼쪽 노드가 가장 큰 경우
          self.heap_array[cur_index], self.heap_array[cur_index * 2] = self.heap_array[cur_index * 2], self.heap_array[cur_index]
          cur_index = cur_index * 2
        else :
          # 왼쪽, 오른쪽, 현재 중 현재가 가장 큰 경우
          break
      else :
        if self.heap_array[cur_index] < self.heap_array[cur_index * 2 + 1] :
          # 왼쪽, 현재, 오른쪽 중 오른쪽이 가장 큰 경우
          self.heap_array[cur_index], self.heap_array[cur_index * 2 + 1] = self.heap_array[cur_index * 2 + 1], self.heap_array[cur_index]
          cur_index = cur_index * 2 + 1
        else :
          # 왼쪽, 현재, 오른쪽 중 현재가 가장 큰 경우
          break
    else : # 왼쪽 자식만 있는 경우
      if self.heap_array[cur_index] < self.heap_array[cur_index * 2] :
          # 왼쪽, 현재 노드 중 왼쪽 노드가 더 큰 경우
          self.heap_array[cur_index], self.heap_array[cur_index * 2] = self.heap_array[cur_index * 2], self.heap_array[cur_index]
          cur_index = cur_index * 2
      else :
        # 왼쪽 현재 중 현재가 가장 큰 경우
        break
  return result
```
