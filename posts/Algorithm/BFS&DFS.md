---
created: 2020-07-23
modified: 2020-07-23
tags: [Algorithm, Search]
title: BFS/DFS
author: Yo0oN
category: Algorithm
---

## 1. BFS 너비 우선 탐색

BFS(Breadth-First Search)는 너비 우선 탐색으로, 그래프 알고리즘 중 하나이다.<br>

![01](https://user-images.githubusercontent.com/53729311/180644547-851105f6-96a0-4fe3-9feb-4174c4704292.jpg)

임의의 노드 하나를 기준으로 잡은 후 해당 노드에서부터 가까이 있는 노드들을 순서로 방문하는 방식으로 탐색을 진행한다.

위의 그림을 보면, 노드 A를 기준으로 해당 노드와 가장 가까운, 간선 하나만으로 이동할 수 있는 B, C를 먼저 탐색한 후, 간선 두개로 이동할 수 있는 D, G, H, I를 탐색하고 있다.

BFS는 두 노드 사이의 최단 경로나, 임의의 경로를 찾고 싶을 때 사용하면 좋다.

BFS는  시간 복잡도는 $$O(V+E)$$로 표현되며, V는 노드, E는 간선이다.

<br>

## 2. BFS 구현하기

BFS는 가장 가까이 있는것부터 순서 상관없이 탐색하기 때문에, 구현 할 때는 ***어떤 노드를 방문했는지 기억해서 순서대로 보여주는 큐***와, ***방문한 노드의 인접 노드들이자, 앞으로 방문해야 할 노드가 적혀있는 큐***를 이용해야 한다.

1. 일단 노드 하나를 기준으로 잡은 후, 큐에 해당 노드를 넣는다.
2. 링크드리스트, 맵, 딕셔너리 등등 값을 저장할 수 있는 자료구조를 하나 선택하여, 키나 인덱스는 하나의 노드, 값은 인접한 노드의 배열을 담는다.
3. 첫번째 노드를 하나 탐색한 후 노드에 넣는다.
4. 탐색한 노드가 키(또는 인덱스)로 있는 값들의 노드들을 큐에 넣고, 앞에서 부터 하나씩 추출하면 탐색한다.
5. 탐색을 하면서, 탐색한 순서가 적힌 리스트에서 이미 다녀온 노드인지 비교하는 작업을 해야한다.
5. 4번과 5번을 반복한다.

```python
def bfs(graph, start_node) :
  visited_queue = list() # 방문한 순서가 들어가는 큐
  need_visit_queue = list() # 방문해야할 노드들이 적혀있는 대기공간 큐
  need_visit_queue.append(start_node) # 처음 기준 노드를 방문할 큐에 넣는다.

  while queue :
    node = need_visit_queue.pop(0) # 큐의 제일 앞에 있는 노드를 추출한다.
    if node not in visited_queue : # 만약 방문하지 않은 노드라면
      visited_queue.append(node) # 방문을하고,
      need_visit_queue.extend(graph[node]) # 방문한 노드의 인접 노드들을 대기 공간인 큐에 넣어준다.

  return visit
```

<br>

## 3. DFS 깊이 우선 탐색

DFS(Depth-First Search)는 깊이 우선 탐색으로, 그래프 알고리즘 중 하나이다.<br>

![02](https://user-images.githubusercontent.com/53729311/180644626-54a2fc8b-102a-476c-ab73-31e60f0aeb5f.jpg)

임의의 노드 하나를 해당 노드의 분기 중 하나를 선택하여 해당 분기를 모두 탐색하고, 다음 분기를 탐색하는 방식으로 탐색한다.

위의 그림을 보면, 노드 A를 기준으로 하나의 분기를 선택하여 B, D, E, F를 모두 탐색한 후, 다음 분기인 C쪽을 탐색하는 것을 볼 수 있다.

주의할 점은 어떤 노드를 방문했는지 여부를 검사하지 않으면 무한루프에 빠질 수 있다.

또, _인간관계에서 A와 B 사이의 관계를 구하시오._ 같은 문제를 풀 때는 DFS를 이용하여 A와 관련된 한사람의 관계를 모두 알게된 후 다음 사람으로 넘어가는 것 보다는, BFS를 이용하여 A의 가까운 관계부터 탐색하는 것이 좋다.

DFS의 시간 복잡도는 $$O(V+E)$$로 표현되며, V는 노드, E는 간선이다.

<br>


## 4. DFS 구현하기

DFS 알고리즘을 구현할 때 주의할 점은 어떤 노드를 방문했었는지 여부를 알아야 한다는 점이다.(그렇지 않으면 무한루프에 빠질수도 있다.)

그렇기 때문에, ***방문한 노드를 차례로 저장하여 차례대로 보여줄 곳은 FIFO인 큐***, ***앞으로 방문할 노드를 저장해며 마지막으로 탐색한 곳의 가지와 이어진 노드를 꺼내줄 곳은 LIFO인 스택***을 이용하여 알고리즘을 구현한다.

![03](https://user-images.githubusercontent.com/53729311/180644634-9290e8f6-3877-415f-a4db-508e621e9469.jpg)

위의 그림을 보면 탐색의 중간까지만 나와있지만 왜 큐와 스택을 사용하는지 알 수 있다.<br>

```python
def bfs(graph, start_node) :
  visited_queue = list() # 방문한 순서가 들어가는 큐
  need_visit_queue = list() # 방문해야할 노드들이 적혀있는 대기공간 큐
  need_visit_queue.append(start_node) # 처음 기준 노드를 방문할 큐에 넣는다.

  while queue :
    node = need_visit_queue.pop(0) # 큐의 제일 앞에 있는 노드를 추출한다.
    if node not in visited_queue : # 만약 방문하지 않은 노드라면
      visited_queue.append(node) # 방문을하고,
      need_visit_queue.extend(graph[node]) # 방문한 노드의 인접 노드들을 대기 공간인 큐에 넣어준다.

  return visit
```
