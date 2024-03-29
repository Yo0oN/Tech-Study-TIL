---
created: 2020-07-10
modified: 2020-07-10
tags: [DataStructure]
title: TreeAndGraph
author: Yo0oN
categories: [DataStructure]
---

## 1. 트리

![01](https://user-images.githubusercontent.com/53729311/180646835-d70907e4-894f-4732-aad1-e3dd4262a8eb.png)

노드를 이용하여 정보를 저장하며, 노드끼리 사이클을 이루지 않는 구조이다.<br>
위의 그림처럼 루트노드부터 가지가 뻗어나와 다른 노드들이 붙어있는 모습이 나무를 닮았다고 하여 트리라고 불린다.<br>
유닉스, 리눅스의 디렉터리 구조도 트리구조이다.

![04](https://user-images.githubusercontent.com/53729311/180646842-98affa01-720f-4558-975a-ae95d75a095d.jpg)
추가적으로 사이클은, 여러 노드와 노드가 이어져있을 때, 간선을 따라 가다보면 처음 정점을 다시 만나는 구조로 처음 정점과, 끝 정점이 같은 경우를 말한다.<br>
하지만 트리는 부모 -> 자식 노드로만 이어져 있기 때문에 처음 정점이 끝 정점이 되는 일은 없기 때문에 사이클을 이루지 않는 구조라 한것이다.

### 1-1. 용어

![02](https://user-images.githubusercontent.com/53729311/180646840-8ddee55c-966b-4df5-9b23-a34be44fd33e.jpg)

- Node(=vertex정점) : 트리에서 데이터를 저장하는 기본 요소. 노드 = 데이터 + 다음 노드의 주소
- Eage(간선) : 노드를 연결하는 선
- Root Node : 트리의 가장 위에 있는 노드
- Leaf Node : 가지의 가장 아래쪽, 즉 자식이 없는 노드
- Level : 루트노드를 0으로 하여 야래쪽의 노드 중 가지를 쳐서 연결된 노드들의 깊이
- Parent Node : 아래로 가지를 뻗어 자식 노드를 가지고 있는 노드
- Child Node : 위에서 가지가 이어져나와 이어져있는 노드
- Depth : 트리에서 노드가 가질 수 있는 최대 레벨

<br>

## 2. 그래프

그래프는 트리처럼 노드와 간선으로 이루어져 있으나, 트리와는 다르게 간선의 방향이 다양하다.<br>
정확히는 트리는 그래프의 한 종류이다. 2-1을 보자.<br>

### 2-1. 그래프의 종류

![06](https://user-images.githubusercontent.com/53729311/180646845-5d4eff6c-86ec-47d5-ac14-d80154d9cf48.jpg)

  1. 무방향 그래프<br>
    방향이 없는 그래프로, 노드와 노드가 간선으로 이루어져 있다면 어느방향이나 상관없이 갈 수 있다.<br>
    간선은 직선으로 표현한다.<br>

  2. 방향 그래프<br>
    간선에 방향이 있는 그래프로, 간선이 화살표로 표현된다. 해당 방향으로만 갈 수 있다.<br>
    표현 할 때 A -> B라면 <A, B>로 표현한다.<br>
    참고로 트리에서도 간선을 직선으로 표현하는데, 편의상 직선으로 표현한것일 뿐, 실제로는 부모에서 자식으로만 방향이 있기 때문에 방향 그래프에 속한다.<br>

  3. 가중치 그래프(네트워크)<br>
    간선이 비용 또는 가중치가 할당된 그래프로, 노드끼리 간선을 타고 이용할 때 비용이 드는 경우를 말한다.<br>
    네트워크라고도 한다.<br>

  4. 연결 그래프<br>
    무방향 그래프에서 모든 노드가 항상 경로가 존재하는 경우를 말한다.<br>
    즉, 모든 노드가 간선을 가지고 있는 경우이다.<br>

  5. 비연결 그래프<br>
    무방향 그래프에서 특정 노드에 대한 경로가 없는 경우를 말한다.<br>

  6. 사이클 그래프<br>
    시작노드와 종료노드가 동일한 경우를 말한다.<br>
    시작과 종료가 같기 때문에, 시작노드에서 출발하면 마지막도 시작노드에서 끝나기 때문에 사이클을 그린다고해서 사이클 그래프이다.<br>

  7. 비 사이클 그래프<br>
    시작노드와 종료노드가 다른경우, 사이클이 없는 경우를 말한다.<br>

  8. 완전그래프<br>
    모든 노드가 서로 연결되어있는 그래프<br>


위의 설명에 따르면 트리는 그래프의 일종으로, 방향 그래프, 연결 그래프, 비 사이클 그래프에 속한다.<br>


### 2-2. 트리와 그래프
| |그래프|트리|
|:--|:--|:--|
|정의|노드와 노드를 연결하는 간선으로 표현되는 자료구조|방향성이 있는 비순환 그래프|
|종류|방향그래프, 무방향그래프, 비연결그래프...다양하게 있다.|방향그래프|
|사이클|사이클이 있는것도, 없는것도 있다.|사이클이 없다.|
|루트노드|루트노드가 없다.|루트노드가 있다.|
|부모&자식|부모와 자식의 개념이 없다.|부모와 자식의 개념이 있다.|

<br>

## 3. 이진트리 & 이진탐색트리

![05](https://user-images.githubusercontent.com/53729311/180646844-6ab07ecb-c5f5-440c-9c0d-384b0fa207f0.jpg)

이진트리는 노드 하나 당 아래로 뻗어나온 가지가 최대 두개까지 있는 트리를 말한다.

이진탐색트리(BST Binary Search Tree)는 이진 트리에서 현재 노드보다 작은 값은 왼쪽, 큰 값은 오른쪽 노드로 가는 조건이 있는 트리이다.<br>
이진탐색트리를 이용하면 값이 이미 정렬되어있기 떄문에 빠르게 원하는 값을 탐색할 수 있다는 장점이 있다.

<br>

## 4. 이진탐색트리 구현하기

### 4-1. 준비

```python
class Node :
  def __init__(self, data) :
    self.data = data
    self.left = None
    self.right = None

class BinarySearchTree :
  def __init__(self, data) :
    self.root = Node(data) # 루트노드에 값을 하나 넣는다.
```

### 4-2. 이진탐색트리에 값 삽입하는 메서드

```python
  def insert(self, data) :
    self.current_node = self.root
    while True :
      # 현재 넣으려는 값이 루트값보다 작을경우 왼쪽으로
      if data < self.current_node.data :
        # 왼쪽노드가 있다면 계속 탐색
        if self.current_node.left != None :
          self.current_node = self.current_node.left
        else : # 없다면 그자리에 값 넣기
          self.current_node.left = Node(data)
          break
      else : # 현재 넣으려는 값이 루트값보다 클경우 오른쪽으로
        if self.current_node.right != None :
          self.current_node = self.current_node.right
        else :
          self.current_node.right = Node(data)
          break
```

### 4-3. 이진탐색트리에서 값이 있는지 찾기

```python
  def search(self, data) :
    self.current_node = self.root
    while self.current_node :
      if self.current_node.data == data :
        return True
      elif data < self.current_node.data :
        self.current_node = self.current_node.left
      else :
        self.current_node = self.current_node.right
    return False
```

### 4-4. 이진트리에서 값 삭제하기

삭제하는 노드가 리프노드라면 다행이지만, 아래에 자식이 있는 부모노드라면 빈자리를 다른 노드가 채워주어야 한다.<br>
경우의 수를 잘 생각해보자.<br>

  1. 자식노드가 없는경우

  2. 삭제하려는 노드의 왼쪽 또는 오른쪽에만 자식이 있을 경우<br>
     삭제할 노드의 왼쪽 또는 오른쪽 자식과 부모를 이어주면 된다.
   
  3. 삭제하려는 노드의 양쪽에 자식이 있을 경우<br>
     이런경우 2가지 방법이 있다.<br>
    3-1. 삭제하려는 노드의 오른쪽 자식 중 가장 작은 자식을 가져와 빈자리에 넣는다.<br>
    3-2. 삭제하려는 노드의 왼쪽 자식 중 가장 큰 자식을 가져와 빈자리에 넣는다.<br>
     하지만 이련경우 가져온 자식에게도 또다른 자식이 있으면 그부분도 처리를 해줘야 한다.
   
위의 3번을 보면 삭제하려는 노드의 오른쪽 또는 왼쪽 자식 중 가장 작은 자식 또는 가장 큰 자식을 가져와 빈자리에 넣는다고 되어있는데, 그 이유는 아래의 그림을 보면 알 수 있다.

![03](https://user-images.githubusercontent.com/53729311/180646841-539f6369-fe4f-4055-b2eb-01295b55ab49.jpg)

3-1. 빈자리를 채우기 위해 아래의 자식들 중 하나를 가져다 써야 하는데 만약 오른쪽 자식 중 하나를 쓴다고 하면, 오른쪽 자식 중 가장 작은값을 빈자리에 넣어야 왼쪽은 부모보다 작고 오른쪽은 부모보다 커야한다는 이진탐색트리의 조건을 만족한다.

3-2 왼쪽자식에서 가져다 쓰는 경우도 마찬가지다.

```python
  def delete(self, data) :
    # 삭제할 노드가 있는지 확인하기
    searched = False # 삭제할 값을 찾았는지 여부를 알려주는 searched
    self.current_node = self.root # 현재노드
    self.parent_node = self.root # 부모노드
    while self.current_node : # 현재 노드가 있는 동안 반복
      # 만약 현재 노드가 삭제하려는 값과 같다면 탐색 중지
      if self.current_node.data == data :
        searched = True
        break
      # 만약 현재 노드가 삭제하려는 값보다 크다면 왼쪽 탐색
      elif data < self.current_node.data :
        self.parent_node = self.current_node
        self.current_node = self.current_node.left
      else : # 현재 노드가 삭제하려는 값보다 작다면 오른쪽으로
        self.parent_node = self.current_node
        self.current_node = self.current_node.right
    if searched == False :
      return False

    # 삭제하려는 값을 찾은 경우 이곳으로들어온다.
    # 1. 만약 삭제하려는 노드가 자식이 없는 리프노드라면..
    if self.current_node.left == None and self.current_node.right == None :
      if data < self.parent_node.data : # 현재 값이 부모의 왼쪽노드라면 
        self.parent_node.left = None # 부모의 왼쪽인 나와 연결 끊기
      else : # 부모의 오른쪽 노드라면
        self.parent_node.right = None # 부모의 오른쪽인 나와 연결 끊기

    # 2. 만약 삭제하려는 노드가 자식노드가 있다면...
    # 2-1. 자식노드가 왼쪽만 있다면
    elif self.current_node.left != None and self.current_node.right == None :
      # 나의 부모와 나의 자식을 이어주자.
      if data < self.parent_node.data : # 2-1-1. 내 자식이 왼쪽
        self.parent_node.left = self.current_node.left
      else : # 2-1-2. 내 자식이 오른쪽
        self.parent_node.right = self.current_node.left
    # 2-2. 자식노드가 오른쪽이라면 
    elif self.current_node.left == None and self.current_node.right != None :
      # 나의 부모와 나의 자식을 이어주자.
      if data < self.parent_node.data : # 2-2-1. 내 자식이 왼쪽
        self.parent_node.left = self.current_node.right
      else : # 2-2-2. 내 자식이 오른쪽
        self.parent_node.right = self.current_node.right

    # 3. 삭제하려는 노드가 자식노드가 두개 있다면...
    elif self.current_node.left != None and self.current_node.right != None :
      if data < self.parent_node.data : # 삭제할 노드가 부모의 왼쪽 자식이었다면
        # 3-1. 삭제하려는 노드의 오른쪽 중 가장 작은 값이 현재 자리에 와야함(혹은 왼쪽 중 가장 큰값)
        self.change_node = self.current_node.right # 빈자리를 채워줄 노드
        self.change_node_parent = self.current_node.right # 빈자리를 채우는 노드의 부모 노드
        while self.change_node.left != None : # 삭제노드의 오른쪽 자식을 탐색하여 가장 작은 값을 찾는다.
          self.change_node_parent = self.change_node
          self.change_node = self.change_node.left
        if self.change_node.right != None : # 옮기려는 자식에 오른쪽 자식이 있다면
          self.change_node_parent.left = self.change_node.right # 옮길자식의 부모와 자식을 이어준다.
        else : # 옮기려는 자식에 오른쪽 자식이 없다면(=리프노드)
          self.change_node_parent.left = None
        self.parent_node.left = self.change_node # 빈자리에 바꿀 노드를 넣는다.
        self.change_node.right = self.current_node.right # 바꾼노드의 오른쪽에 기존에 있던 노드들을 이어준다.
        self.change_node.left = self.change_node.left # 바꾼 노드의 왼쪽에 기존에 있던 노드들을 이어준다.
      else : # 삭제할 노드가 부모의 오른쪽 자식이었다면
        self.change_node = self.current_node.right
        self.change_node_parent = self.current_node.right
        while self.change_node.left != None : # 빈자리를 대신할 노드를 찾기
          self.change_node_parent = self.change_node
          self.change_node = self.change_node.left
        if self.change_node.right != None : # 대신할 노드의 오른쪽에 자식이 있다면
          self.change_node_parent.left = self.change_node.right # 빈자리의 부모-빈자리의 오른쪽 연결
        else : # 옮기려는 자식에 오른쪽 자식이 없다면(=리프노드)
          self.change_node_parent.left = None
        self.parent_node.right = self.change_node # 빈자리에 바꿀 노드를 넣는다.
        self.change_node.right = self.current_node.right # 바꾼 노드의 오른쪽에 기존 노드들을 이어준다. 
        self.change_node.left = self.current_node.left# 바꾼 노드의 왼쪽에 기존에 있던 노드들을 이어준다.
    return True
```

나중에 더 간단하게 작성하는 법을 생각해봐야겠다..
