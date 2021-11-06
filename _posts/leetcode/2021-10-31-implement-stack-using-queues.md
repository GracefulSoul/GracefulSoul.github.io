---
title: "Leetcode Java Implement Stack using Queues"
excerpt: "Leetcode Implement Stack using Queues Java 풀이"
last_modified_at: 2021-10-31T13:00:00
header:
  image: /assets/images/leetcode/implement-stack-using-queues.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - Java

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/problems/implement-stack-using-queues/){:target="_blank"}

# 코드
```java
class MyStack {

  Queue<Integer> main;
  Queue<Integer> sub;

  public MyStack() {
    this.main = new LinkedList<Integer>();
    this.sub = new LinkedList<Integer>();
  }

  public void push(int x) {
    while (!this.main.isEmpty()) {
      this.sub.add(this.main.poll());
    }
    this.main.add(x);
    while (!this.sub.isEmpty()) {
      this.main.add(this.sub.poll());
    }

  }

  public int pop() {
    return this.main.poll();
  }

  public int top() {
    return this.main.peek();
  }

  public boolean empty() {
    return this.main.isEmpty();
  }

}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/579761924/){:target="_blank"}

# 설명
1. queue 2개를 사용하여 [LIFO](https://en.wikipedia.org/wiki/FIFO_and_LIFO_accounting#LIFO){:target="_blank"}의 stack과 같은 MyStack 클래스를 완성하는 문제이다.
- 메서드인 push(int x)는 x를 받아 stack의 위에 넣어준다.
- 메서드인 pop()은 stack의 맨 위에 있는 값을 꺼내 반환한다.
- 메서드인 top()은 stack의 맨 위에 있는 값을 반환한다.
- 메서드인 empty() stack이 비어있는지 유무를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- main은 stack처럼 사용하기 위한 queue이다.
- sub는 main의 값을 역순으로 넣기 위한 queue이다.

3. 주어진 생성자인 MyStack()를 완성한다.
- main과 sub에 LinkedList로 초기화 시켜준다.

4. 주어진 메서드인 push(int x)를 완성한다.
- main에 있는 값을 sub에 순차적으로 넣어주고, main에 x를 먼저 넣어준다.
- 다시 sub에 있는 값을 main에 넣어 순서를 유지시켜준다.
- queue의 경우 [FIFO](https://en.wikipedia.org/wiki/FIFO_and_LIFO_accounting#FIFO){:target="_blank"}이기 때문에, main의 값을 sub로 옮긴 후 main에 주어진 x를 넣고 sub의 값을 main으로 옮기면 LIFO와 같은 효과를 낼 수 있다.

5. 주어진 메서드인 pop()을 완성한다.
- main에 있는 첫 값을 꺼내서 반환한다.

6. 주어진 메서드인 top()을 완성한다.
- main에 있는 첫 값을 꺼내지 않고 반환한다.

7. 주어진 메서드인 empty()를 완성한다.
- main에 비어있는지 여부를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ImplementStackUsingQueues.java){:target="_blank"}에서 확인 가능합니다.