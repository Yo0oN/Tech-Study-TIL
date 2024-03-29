---
created: 2020-08-02
modified: 2020-08-02
tags: [Java, util]
title: java.util.LinkedList
author: Yo0oN
categories: [Java, util]
---

[자료구조의 LinkedList 게시물](https://github.com/Yo0oN/Tech-Study/blob/master/posts/DataStructure/LinkedList.md)
[[LinkedList]]

## 1. LinkedList

LinkedList는 객체를 관리하는데 사용하는 자료구조이다.<br>

![01](https://user-images.githubusercontent.com/53729311/180646967-a218d77c-fac9-4663-989f-af980f55fbf8.jpg)

java.util.LinkedList를 살펴보면 Node라는 것을 이용하여 여러 요소들을 이어주는 것(link)을 볼 수 있다.<br>
Node 하나에는 해당 노드의 값이 들어있고, 앞의 노드와 뒤의 노드를 참조하여 여러 노드들 끼리 이어준다.

보통 자료구조에서 LinkedList라 하면 다음 노드만 참조되어 있어서 앞으로는 가지 못하는데, java.util.LinkedList의 노드를 살펴보면 앞 뒤로 연결되어 있고, 이런것을 DoubleLinkedList라고도 한다.

노드에 값을 저장하기 때문에 Array와는 다르게 중간에 데이터를 삽입, 삭제하는것이 자유롭다.

<br>

## 2. LinkedList의 장단점

LinkedList는 노드를 이용하여 구현되어있기 때문에, 값을 삽입, 삭제할 때 노드의 참조값만 변경해주면 되므로 시간이 적게걸린다는 장점이 있다.<br>
또한 Array처럼 크기가 정해져 있지 않아 메모리를 낭비하지 않으며 메모리가 꽉 차지 않는 한 데이터를 계속 추가할 수 있다.

하지만 값을 가져올 때 Array처럼 값이 연속적으로 있어 인덱스로만 값을 가져오지 않고, 노드를 처음부터 원하는 값이 나올 때 까지 탐색해야 하므로 시간이 오래걸린다는 단점이 있다.

<br>

## 3. java.util.LinkedList 사용법

LinkedList는 List를 implements 하여 만들어 졌기 때문에 ArrayList와 비슷한 메소드들이 많지만 Deque도 implements 하였기 때문에 Deque의 성질도 가지고 있다.<br>
여러 인터페이스를 구현하였기 때문에 비슷한 기능의 다양한 메소드들이 많은데 상황에 맞게 알아서 사용하자.<br>
(Deque : 뒤에다 데이터를 추가하고 앞에서부터 순서대로 반환하는 Queue와는 다르게 앞 뒤 모두에서 데이터의 삽입 삭제가 가능한 Queu로 마치 스택과 비슷하다.)<br>

1. LinkedList 생성하기<br>
```java
LinkedList ll1 = new LinkedList();
LinkedList ll1 = new LinkedList(Collection);
```
첫번째는 크기를 지정해주지 않고 생성해주고,<br>
두번째는 주어진 컬렉션이 저장된 LinkedList를 생성해준다.<br>

2. 값 추가하기<br>
```java
ll1.add(E)
ll1.add(n, E)
ll1.addAll(Collection)
ll1.addAll(n, Collection)
ll1.addFisrt(E)
ll1.addList(E)
ll1.push(E)
```
값을 추가할 때 추가할 값만 입력하면 뒤에서부터 차례로 넣지만, 넣을 위치도 함께 지정해 준다면, 해당 자리에 값을 넣을 수 있다.<br>
또한 Deque처럼 맨 앞과 뒤에 값을 추가할 수 있다.<br>
push는 제일 마지막에 값을 넣어준다.

3. 값 제거하기<br>
```java
ll1.remove(n)
ll1.remove(E)
ll1.removeAll(Collection)
ll1.retainAll(Collection)
ll1.removeLast()
ll1.removeFisrt()
```
값을 제거할 때는 지우려는 위치를 지정하거나, 객체를 지정하여서 제거할 수 있다.<br>
또한, Collection을 매개변수로 넘길 경우 해당 객체를 전부 삭제하지만,<br>
다음 메소드인 retainAll(Collection)을 사용하면 *해당 객체만 제외하고* 나머지를 삭제해준다.<br>
removeLast와 removeFirst는 이름처럼 가장 마지막과 처음 노드를 제거한다.<br>

4. 기타<br>
```java
ll1.get(n)
ll1.subList(n1, n2)
ll1.indexOf(Object)
ll1.lastIndexOf(Object)
ll1.getFirst()
ll1.getLast()
```
해당 위치의 객체를 반환한다.<br>
해당 범위의 객체를 반환한다.<br>
지정된 객체의 위치를 앞에서 부터 찾은 후 제일 처음에 나온 위치를 반환한다.<br>
지정된 객체의 위치를 뒤에서 부터 찾은 후 뒤에서 처음 나온 위치를 반환한다.<br>
첫번째 노드의 객체를 반환한다.<br>
마지막 노드의 객체를 반환한다.<br>

```java
ll1.peek()
ll1.peekFirst()
ll1.peekLast()
ll1.poll()
ll1.pollFisrt()
ll1.pollLast()
ll1.pop()
```
peek과 pop이 붙은 것들은 값을 제거하지 않고, 객체를 반환해주지만, poll이 붙은 것들은 제거한 후 해당 객체를 반환해준다.<br>

```java
ll1.size()
ll1.toArray()
ll1.toArray(Object[])
ll1.contains(Object)
```
해당 LinkedList의 크기를 반환한다.<br>
저장된 모든 객체를 배열로 반환한다.<br>
저장된 모든 객체를 지정 타입의 배열에 반환한다.<br>
찾는 객체가 LinkedList에 들어있는지 여부를 반환한다.
