---
title: "Leetcode Java Design a Stack With Increment Operation"
excerpt: "Leetcode Medium - 'Design a Stack With Increment Operation' 문제 Java 풀이"
last_modified_at: 2024-09-30T17:40:00
header:
  image: /assets/images/leetcode/design-a-stack-with-increment-operation.png
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
[Link](https://leetcode.com/problems/design-a-stack-with-increment-operation/){:target="_blank"}

# 코드
```java
class CustomStack {

  private int[] stack;
  private int top = -1;

  public CustomStack(int maxSize) {
    this.stack = new int[maxSize];
  }

  public void push(int x) {
    if (this.top < this.stack.length - 1) {
      this.top++;
      this.stack[this.top] = x;
    }
  }

  public int pop() {
    if (this.top != -1) {
      return this.stack[this.top--];
    }
    return -1;
  }

  public void increment(int k, int val) {
    for (int i = 0; i < Math.min(k, this.top + 1); i++) {
      this.stack[i] += val;
    }
  }

}

/**
 * Your CustomStack object will be instantiated and called as such:
 * CustomStack obj = new CustomStack(maxSize);
 * obj.push(x);
 * int param_2 = obj.pop();
 * obj.increment(k,val);
 */
```

# 결과
[Link](https://leetcode.com/problems/design-a-stack-with-increment-operation/submissions/1406908209/){:target="_blank"}

# 설명
1. increment 연산자를 제공하는 스택인 CustomStack을 만드는 문제이다.
- 생성자인 CustomStack(int maxSize)은 maxSize 크기의 스택을 초기화한다.
- 메서드인 push(int x)는 스택의 위에 x를 추가한다.
- 메서드인 pop()은 스택의 위에 해당하는 값을 반환한다. 단, 스택이 비어있을 경우 -1을 반환한다.
- 메서드인 increment(int k, int val)는 아래에서 k번째 값까지 val만큼 증가시켜준다. 값이 k개 미만인 경우 모든 값들을 증가시켜준다.

2. CustomStack에 필요한 전역 변수를 정의한다.
- stack은 값을 저장할 변수이다.
- top은 값을 저장한 위치를 저장할 변수이다.

3. 생성자인 CustomStack(int maxSize)을 정의한다.
- stack을 maxSize의 정수 배열로 초기화한다.
- top을 -1로 초기화한다.

4. 메서드인 push(int x)를 정의한다.
- top이 stack의 마지막 위치보다 작은 경우, top을 증가시키고 stack[top]에 x를 넣어준다.

5. 메서드인 pop()을 정의한다.
- top이 -1이 아닌 경우, stack[top]을 반환하고 top을 감소시킨다.
- top이 -1인 경우, 스택의 값이 없으므로 -1을 반환한다.

6. 메서드인 increment(int k, int val)를 정의한다.
- 0부터 k 혹은 $top + 1$ 중 작은 범위 내 값들에 val을 더해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignAStackWithIncrementOperation.java){:target="_blank"}에서 확인 가능합니다.