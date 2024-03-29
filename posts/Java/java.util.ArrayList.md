---
created: 2020-08-01
modified: 2020-08-01
tags: [Java, util]
title: java.util.ArrayList
author: Yo0oN
categories: [Java, util]
---

## 1. ArrayList

ArrayList는객체를 관리하는데 사용하는 자료구조이다.<br>

![01](https://user-images.githubusercontent.com/53729311/180646941-c161acbe-be3b-4723-ab50-9f3477022a5f.jpg)

java.util.ArrayList를 살펴보면 내부적으로는 **배열**을 이용하여 구현되어있다.<br>

![02](https://user-images.githubusercontent.com/53729311/180646943-31958f21-74b4-46ee-9590-9aa6b169cd58.jpg)

하지만 Array(배열)과는 다르게 용량이 다 차게 된다면 내부적으로 더 큰 배열을 만들어 크기를 키운 후 값을 더 넣을 수 있다. (=***Dynamic***)<br>
(물론 무한히 넣을 수 있는것은 아니고 int의 최댓값인 0x7fffffff 까지만 크기를 키울 수 있다.)<br>

![03](https://user-images.githubusercontent.com/53729311/180646944-cd00cfb9-9c31-4a6b-8c7d-ce31adbd6f5b.jpg)

또한, 값을 자리가 있는 경우 마지막에만 추가해 줄 수 있는 배열과는 다르게, 사이에 끼워 넣을 수도 있다.<br>
그럴경우, 이전에 있던 값들을 한칸씩 뒤로 옮긴 후 넣게된다.

데이터를 빼는 경우에도 마찬가지로, 값을 제거하면 제거한 값의 뒤에서부터 앞으로 한칸씩 자리를 이동하여 빈자리를 메꿔준다.<br>
(참고로 값을 추가할 때 크기를 키운것과는 다르게 제거한다고 해서 크기를 줄이지는 않는다.)

<br>

## 2. ArrayList의 장단점

ArrayList는 배열을 이용하여 구현되어있기 때문에, 접근할 때 인덱스를 이용하여 접근하여 빠르게 원하는 값을 찾을 수 있다.<br>
또한 크기가 변하기 때문에 값을 계속해서 추가할 수 있다는 장점이 있다.

하지만 그와 반대로 삽입, 삭제가 일어날 때마다 다른 값들의 위치를 이동시키기 때문에 시간이 오래걸릴 뿐더러, 크기를 키웠는데 그만큼의 값을 추가하지 않을 경우에는 메모리 낭비가 있다는 단점도 있다.

<br>

## 3. java.util.ArrayList 사용법

1. ArrayList 생성하기<br>
```java
ArrayList al1 = new ArrayList();
ArrayList al2 = new ArrayList(크기);
ArrayList al3 = new ArrayList(Collection);
```
첫번째는 크기를 지정해주지 않고 생성해주고,<br>
두번째는 크기를 지정한 후 생성하며,<br>
세번째는 주어진 컬렉션이 저장된 ArrayList를 생성해준다.

2. 값 추가하기<br>
```java
al1.add(value)
al1.add(index, value)
al1.addAll(Collection)
al1.addAll(index, Collection)
```
값을 추가할 때 추가할 값만 입력하면 뒤에서부터 차례로 넣지만, 넣을 위치도 함께 지정해 준다면, 해당 자리에 값을 넣고, 이전에 있던 값들은 한칸씩 뒤로 밀려나게 된다.

3. 값 제거하기<br>
```java
al1.remove(index)
al1.remove(Object)
al1.removeAll(Collection)
al1.retainAll(Collection)
```
값을 제거할 때는 지우려는 위치를 지정하거나, 객체를 지정하여서 제거할 수 있다.<br>
또한, Collection을 매개변수로 넘길 경우 해당 객체를 전부 삭제하지만,<br>
마지막 메소드인 retainAll(Collection)을 사용하면 *해당 객체만 제외하고* 나머지를 삭제해준다.

4. 기타<br>
```java
al1.set(index, value)
```
해당 위치의 객체를 바꿔준다.
```java
al1.get(index)
al1.subList(inedex1, index2)
al1.indexOf(Object)
al1.lastIndexOf(Object)
```
위에서부터 차례로<br>
해당 위치의 객체를 반환한다.<br>
해당 범위의 객체를 반환한다.<br>
지정된 객체의 위치를 앞에서 부터 찾은 후 제일 처음에 나온 위치를 반환한다.<br>
지정된 객체의 위치를 뒤에서 부터 찾은 후 뒤에서 처음 나온 위치를 반환한다.
```java
al1.size()
al1.toArray()
al1.toArray(Object[])
```
해당 ArrayList의 크기를 반환한다.<br>
저장된 모든 객체를 배열로 반환한다.<br>
저장된 모든 객체를 지정 타입의 배열에 반환한다.

<br>

위의 메소드들 외에 다른 메소드들도 있으니 [Java API](https://docs.oracle.com/en/java/javase/13/docs/api/java.base/java/util/ArrayList.html) 를 찾아보자.
