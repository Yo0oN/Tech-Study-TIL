---
created: 2020-07-02
modified: 2020-07-02
tags: [DataStructure]
title: Queue
author: Yo0oN
categories: [DataStructure]
---

## 1. Queue 큐

큐는 스택과 반대로 먼저 들어온 것이 먼저 나간다는 특징을 가지고 있다.

마트에서 줄을 설 때 먼저 서 있는 순서대로 계산을 한다는것과 같다.

보통 멀티태스킹을 위한 스케쥴링이나 버퍼에서 사용한다.

> FIFO(First In First Out) / LILO(Last In Last Out)

큐도 배열을 이용하여 간단하게 구현할 수 있다는 장점이 있지만 대신 크기가 미리 정해지면 메모리 낭비가 발생한다는 단점이 있다.

또한 앞에서부터 넣은 후 빼다보면 배열의 앞쪽에는 공간이 있음에도 더이상 활용할 수 없다는 단점도 존재한다.

이를 대비하여 위하여 큐의 처음과 마지막이 이어져있는 원형 큐라는 것도 존재한다.


### 1-1. 원형큐

일반적인 큐의 단점을 보완한 것으로 큐의 처음과 마지막을 이어주어 큐의 마지막까지 rear가 도달하더라도 다시 처음으로 돌아가 데이터를 넣고 뺄 수 있다.

![01](https://user-images.githubusercontent.com/53729311/180646804-d1e3b633-69ca-48ce-b4b2-4f8635273870.png)

그리고 원형 큐는 한 칸을 비어두어 현재 큐가 포화상태인지, 공백상태인지 알 수 있다.

![02](https://user-images.githubusercontent.com/53729311/180646807-b81aa434-29da-4d51-bc4c-78991bdc0265.jpg)

만약 front == rear라면 현재 공백상태이고, rear가 front보다 한칸 뒤에 있다면 포화상태이다.

큐의 전 부분을 계속 사용할 수 있다는 장점이 있지만, 이런 원형 큐에도 크기가 고정되어있을 수 밖에 없다는 단점이 아직 있다.

### 1-2. LinkedList 큐

LinkedList나 ArrayList처럼 크기가 고정되어 있지 않다면 이를 이용하여 큐를 구현할 수 있다.

아래의 2-1번에서는 LinkedList를 이용하여 큐를 구현하고 있다.


### 1-3. Queue의 기능들

참고로 큐에서는 가장 첫번째 원소를 front, 마지막 원소를 rear라 부른다.

<table>
  <tr>
    <td>enQueue</td>
    <td>데이터를 넣는다.</td>
  </tr>
    <tr>
    <td>deQueue</td>
    <td>데이터를 뺀다.</td>
  </tr>
    <tr>
    <td>isEmpty</td>
    <td>큐가 비어있는지 확인한다.</td>
  </tr>
    <tr>
    <td>isFull</td>
    <td>큐가 꽉 차있는지 확인한다.</td>
  </tr>
</table>

<br>

## 2. 구현하기

### 2-1. LinkedList를 이용하여 구현하기 - Python

```python
class Queue :
  class Node : # 노드 내부에는 값과, 다음 노드가 있다.
    def __init__(self, data) :
      self.data = data
      self.next = None
      
  def __init__ (self) :
    self.front = None # 처음 만들어 졌을 때는 큐의 처음과 마지막이 비어있다.
    self.rear = None

  def enque(self, data) : # 데이터를 넣어주는 enque
    self.node = Node(data) # 노드를 생성한다.
    if self.rear !=None : # 만약 큐에 데이터가 있다면
      self.rear.next = self.node # 마지막의 다음에 현재 노드를 붙인다.
    self.rear = self.node # 현재 노드는 마지막 노드가 된다.
    if self.front == None : # 그런데 큐에 데이터가 없다면
      self.front = self.node # 처음 노드를 현재 노드로도 해준다.
    
  def deque(self) : # 데이터를 빼주는 deque
    if (self.front == None) : # 데이터가 없다면
      return False # False를 반환한다.
    result = self.front.data # 데이터가 있다면 데이터를 일단 뺀 후
    self.front = self.front.next # 두번째 노드를 처음으로 옮긴다.
    return result

  def peek(self) : # 데이터를 보여주는 peek
    if (self.front) == None : # 데이터가 없다면
      return False # False를 반환한다.
    return self.front.data # 데이터가 있다면 보여준다.
 
  def isEmpty (self): # 큐가 비었는지 확인하는 isEmpty
    return self.front == None

  def clear (self): # 큐를 비워주는 clear
    self.front = None
    self.rear = None

    # 현재 큐는 링크드리스트로 만들어졌기 때문에 isFull이 필요 없다.
```


### 2-2. 원형 큐 구현하기 - Java

```java
class Queue<T> {
	int front = 0; // 처음 위치를 알려주는 front
	int rear = 0; // 마지막 포인트를 알려주는 rear
	int size = 0; // 큐의 크기
	T[] que = null; // 데이터가 들어갈 배열
	
	public Queue(int size) {
		// 큐는 공백, 포화를 구분하기 위해 자리를 하나 비워두어야 하니 한칸크게 만들어주자.
		// 그리고 front에는 값이 없는상태로 유지된다.
		this.size = size + 1; 
		// 데이터가 들어갈 배열을 만든다.
		this.que = (T[]) new Object[this.size];
	}
	public void enque(T data) {
		if (isFull()) {
			// 만약 다 차있다면 넣을 수 없다.
			System.out.println("Queue가 포화상태 입니다.");
			return;
		}
		++rear; // 데이터를 넣기 전 rear의 위치를 한칸 옮긴다.
		// rear가 마지막+1이 되었다면 rear위치를 1로 다시 변경해야하니 rear % size를 통하여 변경한다.
		rear = rear % size;
		que[rear] = data;
	}
	public T deque() {
		if (isEmpty()) {
			// 만약 비어있다면 null을 반환한다.
			System.out.println("Queue가 공백상태 입니다.");
			return null;
		}
		++front; // front에는 값이 없으므로 값이 있는 앞으로 한칸 간다. 
		front = front % size; // front % size를 통해 위치 조정.
		T result = que[front];
		return result;
	}
	public boolean isEmpty() {
		// front == rear면 공백상태이다.
		return front ==rear;
	}
	public boolean isFull() {
		// rear가 front의 바로 뒤에 있다면 포화 상태이다.
		// rear + 1을 통하여 rear를 한칸 앞으로 옮기고,
		// % size를 통하여 rear 위치를 조정해주었을 때 front 같다면 포화이다.
		return ((rear + 1) % size == front);
	}
}
```
