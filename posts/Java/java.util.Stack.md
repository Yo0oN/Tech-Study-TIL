---
created: 2020-08-08
modified: 2020-08-08
tags: [Java, util]
title: java.util.Stack
author: Yo0oN
categories: [Java, util]
---

[자료구조의 Stack 게시물](https://github.com/Yo0oN/Tech-Study/blob/Yo0oN-patch-2/posts/DataStructure/Stack.md)

## 1. Stack

Stack은 먼저 마지막으로 들어간것이 먼저 나오는(LILO / FILO) 자료구조이다.<br>

![01](https://user-images.githubusercontent.com/53729311/180646979-14ad09fb-b17f-4dfc-8fbe-0c14119c8869.png)

Stack은 Vector 클래스를 상속받았으며, java.util.Stack를 내부에서 Stack을 구현하는부분을 따라가다 보면 Vector 클래스로 이어지고 있다.<br>
그리고 Vector의 내부에서는 배열을 이용하여 값을 저장중이다.

<br>

## 2. java.util.Stack 사용법

Stack은 메소드가 많이없다.

1. Stack 생성하기<br>
```java
Stack s = new Stack();
```
Stack은 생성자가 하나만 있다.

2. 값 추가 + 빼기
```java
empty()
peek()
pop()
push(E item)
search(Object o)
```
위에서부터 차례로 스택이 비어있는지 확인하는것,<br>
가장 위의 데이터를 리턴해주는 메서드,<br>
가장 위의 데이터를 리턴하고 지워주는 메서드,<br>
가장 위에 값을 저장하는 메서드,<br>
매개변수로 넘어간 객체의 위치를 리턴해주는 메서드이다.
