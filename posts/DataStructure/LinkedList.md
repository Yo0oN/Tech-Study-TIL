---
created: 2020-07-06
modified: 2020-07-06
tags: [DataStructure]
title: LinkedList
author: Yo0oN
categories: [DataStructure]
---

## 1. Linked List

링크드리스트, 연결리스트 라고도 불린다.

배열과 비교되는 자료구조인데, 배열은 일정 저장 공간에 데이터를 연속적으로 저장을 한다.<br>
하지만 링크드리스트는 데이터와 데이터가 멀리 떨어져있어도 주소를 이용하여 연결할 수 있다.

![01](https://user-images.githubusercontent.com/53729311/180646794-2ae541a5-6f7b-492a-b547-d9fcc1e3bd2b.jpg)

그림에서 보이듯 배열은 저장공간이 지정되어있어서 데이터를 추가하려면 더 큰 배열로 옮겨야하지만,<br>
링크드리스트는 데이터들끼리 떨어져있어도 주소만 알고 연결해주면 되기 때문에 데이터를 추가하는데 어려움이 없다.

하지만, 링크드리스트의 이런 특징은 단점이 되기도 하는데,<br>
인덱스로 값에 접근이 가능한 배열과는 다르게 접근할 수 있는 방법이 앞에서부터 하나씩 탐색하는 것 뿐이라 시간이 오래걸릴수밖에 없다.


### 1-1. 노드

![02](https://user-images.githubusercontent.com/53729311/180646796-03091b5f-5be2-4031-8a29-fa3705977e65.jpg)

자료구조에는 Node(노드)라는 단위가 있는데, 하나의 정보를 저장하고 있는 단위를 뜻한다.<br>
노드에는 정보와, 다음 노드에 대한 연결을위한 정보를 가지고 있고,<br>
링크드리스트에서도 데이터 하나 하나가 저장된 곳을 노드라고 한다.<br>
(이후의 다른 자료구조에서도 노드는 자주 나온다.)

<br>

## 2. 구현하기 - Python

```python
class Node :
  def __init__(self, data, next = None) :
    self.data = data
    self.next = next

class LinkedList :
  def __init__(self, data) :
    # 일단 링크드리스트를 구현할 때 데이터를 하나 넣어야한다.
    self.head = Node(data)

  # 링크드리스트의 마지막에 값을 넣는 append
  def append(self, data) :
    # 혹시라도 head값이 없다면 head에 추가
    # (링크드리스트 구현시 head를 만들어 두긴하지만, 혹시 모를 상황을 위하여)
    if self.head == '' :
      self.head = Node(data)
      return True
    else :
      node = self.head
      # 노드의 마지막까지 간다.
      while node.next :
        node = node.next
      # 마지막 노드의 다음에 값을 넣어준다.
      node.next = Node(data)
      return True

  # 링크드리스트의 처음에 값을 넣는 push
  def push(self, data) :
    node = Node(data)
    if self.head != None : # head가 있다면 head를 다음으로 옮기고 진행
      node.next = self.head
    self.head = node
    return True

  # 링크드리스트의 특정 값 뒤에 값을 넣는 insertAfter
  def insertAfter(self, prev_data, data) :
    if self.head == None : # head가 없다면 head에 추가
      self.head = Node(data)
      return True
    # head가 있다면 아래 진행
    node = self.head
    while node.data != pre_data : # 노드의 값이 특정값과 같을 때까지 반복
      if node.next == None : # 만약 노드의 다음이 비어있다면 특정값이 없으므로 중단
        print("찾는 값이 없습니다.")
        return False # False 반환
      node = node.next # 아니라면 다음노드 계속 탐색
    new_node = Node(data)
    if node.next == None :
      node.next = new_node # 만약 특정값이 담긴 노드가 마지막이었다면 그냥 추가
      return True
    else : # 만약 마지막이 아니라면 다음 노드 이동 후 추가
      new_node.next = node.next
      node.next = new_node.next
      return True

  # 링크드리스트를 순회하는 desc
  def desc(self) :
    node = self.head
    while node :
      print(node.data)
      node = node.next
    
  # 노드를 삭제하는 delete
  def delete(self, delnum) :
    # 만약 head가 비어있다면 그대로 종료
    if self.head == None :
      return False
    if delnum == self.head.data : # head를 삭제할 경우
      temp = self.head
      self.head = self.head.next
      del temp
      return True
    else : # 삭제할 것이 head가 아니라 중간, 마지막이라면
      node = self.head
      while node.next : # 링크드리스트를 앞에서부터 살펴본다.
        # 만약 다음 노드의 값이 삭제할 값이라면..
        if node.next.data == delnum :
          # 삭제할 값을 따로 빼둔다.
          temp = node.next
          # 다음 노드를 다다음 노드로 바꿔준다.
          node.next = node.next.next
          # 삭제한 후 반복문 중단.
          del temp
          return True
        else : # 다음 노드가 삭제할 값이 아니라면 
          node = node.next
      print('삭제할 값이 없습니다.')
      return False
```
