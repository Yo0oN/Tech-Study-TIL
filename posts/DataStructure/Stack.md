---
created: 2020-07-01
modified: 2020-07-01
tags: [DataStructure]
title: Stack
author: Yo0oN
categories: [DataStructure]
---

## 1. Stack

Stack은 데이터를 저장하는데 사용되는 구조로, 가장 마지막에 넣은 것이 가장 처음으로 나간다.

여러 권의 책을 쌓은 후 아래가 아닌, 위에서부터 한 권씩 빼서 사용하는 것과 같은 원리이다.

> LIFO(Last In Firt Out) / FILO(First In Last Out)

<br>

Stack은 보통 배열 구조를 활용하여 쉽게 구현 할 수 있다는 장점이 있지만,

이렇게 할 경우 Stack의 크기를 미리 정해주어야 하며, 그만큼 낭비가 발생할 수 있다는 단점이 있다.


### 1-1. Stack의 기능들

<table>
  <tr>
    <td>기능</td>
    <td>설명</td>
  </tr>
  
  <tr>
    <td>push</td>
    <td>데이터를 스택에 넣는다.</td>
  </tr>
  
  <tr>
    <td>pop</td>
    <td>데이터를 스택에서 꺼낸다.</td>
  </tr>
  
  <tr>
    <td>peek</td>
    <td>데이터를 꺼내지 않고 보기만 한다.</td>
  </tr>
  
  <tr>
    <td>clear</td>
    <td>모든 요소를 삭제한다.</td>
  </tr>
  
  <tr>
    <td>dump</td>
    <td> 모든 데이터를 보여준다.</td>
  </tr>
  
  <tr>
    <td>isEmpty</td>
    <td>스택이 비었는지 알려준다.</td>
  </tr>
</table>

<br>

## 2-1. 구현해보기 - Python

```python
class Stack :
  class Node : # Node 내부에는 값과, 다음 노드가 있다.
    def __init__(self, data) :
      self.data = data
      self.next = None
      
  def __init__(self) : # Stack을 처음 만들었을 때에는 값이 아무것도 있지 않다.
    self.last = None
  
  def push(self, data) : # Stack에 값을 넣어주는 push
    self.node = Node(data) # 노드를 생성해서 값을 넣어준다.
    self.node.next = self.last # 노드의 다음 노드는 이전에 상단에 있던 Node가 온다.
    self.last = self.node # 새로 생성된 노드가 위로 올라간다.

  def pop(self) : # Stack에서 값을 빼서 보여주는 pop
    if (self.last == None) : # 만약 Stack에 아무것도 없다면 None을 반환한다.
      return None
    result = self.last.data # 가장 마지막 데이터를 보여준다.
    self.last = self.last.next # 마지막 데이터가 빠졌으니 이전 노드가 상단으로 와야한다.
    return result

  def peek(self) :
    if (self.last == None) : # 만약 Stack에 아무것도 없다면 None을 반환한다.
      return None
    return self.last.data # 가장 마지막의 데이터를 보여준다.
    
  def isEmpty(self) : # Stack이 비었는지 알려주는 isEmpty
    return self.last == None
    
  def clear(self) : # Stack을 비워주는 clear
    self.last = None
```

<hr>

## 2-2. 구현해보기 - Java

Java로는 기본 기능인 push, pop, peek만 구현했습니다.

```java
import java.util.NoSuchElementException;

class Stack<T> {
  // 하나의 노드에는 하나의 값과 다음 노드가 담겨있다.
  class Node<T> {
    private T data;
    private Node<T> next;
    public Node(T data) {
      this.data = data
    }
  }
  
  // 가장 위의 데이터가 담긴 노드
  private Node<T> last;
  
  // 스택에 값을 넣는 push 스텍
  public push(T data) {
    // 노드를 생성하여 값을 넣고
    Node<T> node = new Node<T>(data);
    // 이전에 있던 가장 위의 노드를 새로운 노드의 다음으로 설정해 준다.
    node.next = last;
    // 가장 위의 노드를 새로운 노드로 설정해 준다.
    last = node;
  }
  
  // 스택에서 값을 빼는 pop
  public T pop() {
    // 만약 스택에 값이 아무것도 없다면 예외처리
    if (last == null) {
      throw new NoSuchElementException("pop 실패. 데이터가 없습니다.");
    }
    T result = last.data;
    last = last.next;
    return result;
  }
  
  // 스택에서 마지막 값을 보여주는 peek
  public T peek() {
    // 만약 스택에 값이 아무것도 없다면 예외처리
    if (last == null) {
      throw new NoSuchElementException("pop 실패. 데이터가 없습니다.");
    }
    return last.data;
  }
}
```

참고로 Java에는 java.util.Stack 클래스가 존재한다.

대신 Stack 클래스에서는 값을 넣는 메소드가 add() 이고, 아래와 같이 사용한다.

```ava
import java.util.Stack;

public class Main{
  public static void main(String[] args){
    Stack<Integer> stack = new Stack<Integer>();
    stack.add(1);
    stack.pop(); // 1
  }
}
```
