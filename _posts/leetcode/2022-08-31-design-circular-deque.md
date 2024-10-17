---
title: "Leetcode Java Design Circular Deque"
excerpt: "Leetcode - 'Design Circular Deque' 문제 Java 풀이"
last_modified_at: 2022-08-31T19:20:00
header:
  image: /assets/images/leetcode/design-circular-deque.png
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
[Link](https://leetcode.com/problems/design-circular-deque/){:target="_blank"}

# 코드
```java
class MyCircularDeque {

  private int[] deque;

  private int front;
  private int rear;

  private int max;
  private int size;

  public MyCircularDeque(int k) {
    this.deque = new int[k];
    this.max = k;
    this.rear = 1;
  }

  public boolean insertFront(int value) {
    if (this.isFull()) {
      return false;
    } else {
      this.front = (this.front + 1) % this.max;
      this.deque[this.front] = value;
      this.size++;
      return true;
    }
  }

  public boolean insertLast(int value) {
    if (this.isFull()) {
      return false;
    } else {
      this.rear = ((this.rear - 1) + this.max) % this.max;
      this.deque[this.rear] = value;
      this.size++;
      return true;
    }
  }

  public boolean deleteFront() {
    if (this.isEmpty()) {
      return false;
    } else {
      this.front = ((this.front - 1) + this.max) % this.max;
      this.size--;
      return true;
    }
  }

  public boolean deleteLast() {
    if (this.isEmpty()) {
      return false;
    } else {
      this.rear = (this.rear + 1) % this.max;
      this.size--;
      return true;
    }
  }

  public int getFront() {
    return this.size == 0 ? -1 : this.deque[this.front];
  }

  public int getRear() {
    return this.size == 0 ? -1 : this.deque[this.rear];
  }

  public boolean isEmpty() {
    return this.size == 0;
  }

  public boolean isFull() {
    return this.size == this.max;
  }

}

/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * MyCircularDeque obj = new MyCircularDeque(k);
 * boolean param_1 = obj.insertFront(value);
 * boolean param_2 = obj.insertLast(value);
 * boolean param_3 = obj.deleteFront();
 * boolean param_4 = obj.deleteLast();
 * int param_5 = obj.getFront();
 * int param_6 = obj.getRear();
 * boolean param_7 = obj.isEmpty();
 * boolean param_8 = obj.isFull();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/787905199/){:target="_blank"}

# 설명
1. 지난 번 [Design Circular Queue](../design-circular-queue){:target="_blank"}와 유사하게 아래의 구조의 순환되는 Deque를 구현하는 문제이다.
- 생성자인 MyCircularDeque(int k)는 Deque 크기인 k를 이용하여 객체를 초기화한다.
- 메서드인 insertFront()는 Deque의 앞에 입력된 값을 넣어주는 역할을 수행하며, 성공했는지 결과를 boolean 값으로 반환한다.
- 메서드인 insertLast()는 Deque의 뒤에 입력된 값을 넣어주는 역할을 수행하며, 성공했는지 결과를 boolean 값으로 반환한다.
- 메서드인 deleteFront()는 Deque의 앞에 입력된 값을 제거하는 역할을 수행하며, 성공했는지 결과를 boolean 값으로 반환한다.
- 메서드인 deleteLast()는 Deque의 뒤에 입력된 값을 제거하는 역할을 수행하며, 성공했는지 결과를 boolean 값으로 반환한다.
- 메서드인 getFront()는 Deque의 앞에 있는 값을 반환하는 역할을 수행하며, 비어있으면 -1을 반환한다.
- 메서드인 getRear()는 Deque의 뒤에 있는 값을 반환하는 역할을 수행하며, 비어있으면 -1을 반환한다.
- 메서드인 isEmpty()는 Deque가 비어있는지 검증하는 역할을 수행한다.
- 메서드인 isFull()은 Deque가 꽉 차있는지 검증하는 역할을 수행한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- deque는 입력된 값들을 순환되는 Deque로 관리하기 위한 배열이다.
- front와 rear는 입력된 값 중 가장 앞과 뒤에 입력된 값을 저장하는 변수이다.
- max는 deque의 최대 크기를 저장할 변수이다.
- size는 deque의 현재 크기를 저장할 변수이다.

3. 생성자인 MyCircularDeque(int k)를 정의한다.
- deque를 입력된 k 크기인 정수 배열로 초기화한다.
- max에 k를 넣어 보관한다.
- rear는 초기 값인 1을 넣어 초기화한다.

4. 메서드인 insertFront()를 정의한다.
- 11번에서 정의한 isFull() 메서드를 수행하여 deque가 꽉 차있는 경우 입력이 불가능하므로, false를 반환한다.
- 위의 경우가 아니라면 아래를 수행한다.
  - front에 overflow를 방지하기 위해 $front + 1$에서 max를 나눈 나머지 값을 넣어준다.
  - deque의 front번째 위치에 value를 넣어주고, size를 증가시킨다.
  - 정상적으로 value를 deque의 앞에 저장하였으므로, true를 반환한다.

5. 메서드인 insertLast()를 정의한다.
- 11번에서 정의한 isFull() 메서드를 수행하여 deque가 꽉 차있는 경우 입력이 불가능하므로, false를 반환한다.
- 위의 경우가 아니라면 아래를 수행한다.
  - rear에 overflow를 방지하기 위해 $(rear - 1) + max$에서 max를 나눈 나머지 값을 넣어준다.
  - deque의 rear번째 위치에 value를 넣어주고, size를 증가시킨다.
  - 정상적으로 value를 deque의 뒤에 저장하였으므로, true를 반환한다.

6. 메서드인 deleteFront()를 정의한다.
- 10번에서 정의한 isEmpty() 메서드를 수행하여 deque가 비어있는 경우 값이 없으므로, false를 반환한다.
- 위의 경우가 아니라면 아래를 수행한다.
  - front에 overflow를 방지하기 위해 $(front - 1) + max$에 max를 나눈 나머지 값을 넣어준다.
  - size를 감소시켜 현재 크기를 감소시킨다.
  - 정상적으로 deque의 앞의 값을 제거하였으므로, true를 반환한다.

7. 메서드인 deleteLast()를 정의한다.
- 10번에서 정의한 isEmpty() 메서드를 수행하여 deque가 비어있는 경우 값이 없으므로, false를 반환한다.
- 위의 경우가 아니라면 아래를 수행한다.
  - rear에 overflow를 방지하기 위해 $rear + 1$에 max를 나눈 나머지 값을 넣어준다.
  - size를 감소시켜 현재 크기를 감소시킨다.
  - 정상적으로 deque의 뒤의 값을 제거하였으므로, true를 반환한다.

8. 메서드인 getFront()를 정의한다.
- 10번에서 정의한 isEmpty() 메서드를 수행하여 deque가 비어있는 경우 값이 없으므로, -1을 반환한다.
- 위의 경우가 아니라면 deque의 front번째 값을 반환한다.

9. 메서드인 getRear()를 정의한다.
- 10번에서 정의한 isEmpty() 메서드를 수행하여 deque가 비어있는 경우 값이 없으므로, -1을 반환한다.
- 위의 경우가 아니라면 deque의 rear번째 값을 반환한다.

10. 메서드인 isEmpty()를 정의한다.
- size가 0인지를 검증한 결과를 반환한다.

11. 메서드인 isFull()를 정의한다.
- size가 max인지를 검증한 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignCircularDeque.java){:target="_blank"}에서 확인 가능합니다.