---
title: "Leetcode Java Implement Queue using Stacks"
excerpt: "Leetcode Implement Queue using Stacks Java 풀이"
last_modified_at: 2021-11-07T01:30:00
header:
  image: /assets/images/leetcode/implement-queue-using-stacks.png
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
[Link](https://leetcode.com/problems/implement-queue-using-stacks/){:target="_blank"}

# 코드
```java
class MyQueue {

  private Stack<Integer> input;
  private Stack<Integer> output;

  public MyQueue() {
    this.input = new Stack<>();
    this.output = new Stack<>();
  }

  public void push(int x) {
    this.input.push(x);
  }

  public int pop() {
    this.move();
    return this.output.pop();
  }

  public int peek() {
    this.move();
    return this.output.peek();
  }

  public boolean empty() {
    return this.input.empty() && this.output.empty();
  }

  private void move() {
    if (this.output.empty()) {
      while (!this.input.empty()) {
        this.output.push(this.input.pop());
      }
    }
  }

}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/582968569/){:target="_blank"}

# 설명
1. 지난 [Implement Stack using Queues](../implement-stack-using-queues){:target="_blank"}와 반대되는 문제로, Stack 2개를 사용하여 [FIFO](https://en.wikipedia.org/wiki/FIFO_and_LIFO_accounting#FIFO){:target="_blank"}의 queue와 같은 MyQueue 클래스를 완성하는 문제이다.
- 메서드인 push(int x)는 x를 받아 queue에 넣어준다.
- 메서드인 pop()은 queue의 맨 앞에 있는 값을 꺼내 반환한다.
- 메서드인 peek()는 queue의 맨 앞에 있는 값을 반환한다.
- 메서드인 empty()는 queue가 비어있는지 여부를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- input은 값이 들어오면 들어갈 stack이다.
- output은 값이 들어온 MyQueue의 값을 반환하기 위한 stack이다.

3. 주어진 생성자인 MyQueue()를 완성한다.
- input과 output에 Stack으로 초기화 시켜준다.

4. 주어진 메서드인 push(int x)를 완성한다.
- input에 주어진 x 값을 넣어준다.

5. 주어진 메서드인 pop()과 peek()를 사용하기 전에 input의 값을 output으로 이동하기 위한 move() 메서드를 완성한다.
- output이 비어있을 경우, input의 값들을 모두 꺼내서 output에 넣어 역순으로 정렬시켜준다.
- stack의 경우 [LIFO](https://en.wikipedia.org/wiki/FIFO_and_LIFO_accounting#LIFO){:target="_blank"}이기 때문에, input에 있는 값을 output에 넣으면 거꾸로 쌓이게 되어 Queue와 같이 순차적으로 FIFO와 같은 효과를 낼 수 있다.

6. 주어진 메서드인 pop()을 완성한다.
- 5번에서 정의한 move() 메서드를 수행하여 값을 역순으로 정렬한다.
- output에 있는 가장 위의 값을 꺼내서 반환한다.

7. 주어진 메서드인 peek()를 완성한다.
- 5번에서 정의한 move() 메서드를 수행하여 값을 역순으로 정렬한다.
- output에 있는 가장 위의 값을 반환한다.

8. 주어진 메서드인 empty()를 완성한다.
- input과 output 두 개의 stack이 모두 비어있는지 여부를 반환한다.
- input으로 들어온 값을 output에서 다 쓴 경우, 남아있는 값이 없으므로 비어있다고 볼 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ImplementQueueUsingStacks.java){:target="_blank"}에서 확인 가능합니다.