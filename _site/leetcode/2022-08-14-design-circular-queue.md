---
title: "Leetcode Java Design Circular Queue"
excerpt: "Leetcode Design Circular Queue Java"
last_modified_at: 2022-08-14T09:30:00
header:
  image: /assets/images/leetcode/design-circular-queue.png
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
[Link](https://leetcode.com/problems/design-circular-queue/){:target="_blank"}

# 코드
```java
class MyCircularQueue {

  private final int[] array;
  private int front;
  private int rear;
  private int length;

  public MyCircularQueue(int k) {
    this.array = new int[k];
    this.front = 0;
    this.rear = -1;
    this.length = 0;
  }

  public boolean enQueue(int val) {
    if (!this.isFull()) {
      this.rear = (this.rear + 1) % this.array.length;
      this.array[this.rear] = val;
      this.length++;
      return true;
    } else {
      return false;
    }
  }

  public boolean deQueue() {
    if (!this.isEmpty()) {
      this.front = (this.front + 1) % this.array.length;
      this.length--;
      return true;
    } else {
      return false;
    }
  }

  public int Front() {
    return this.isEmpty() ? -1 : this.array[this.front];
  }

  public int Rear() {
    return this.isEmpty() ? -1 : this.array[this.rear];
  }

  public boolean isEmpty() {
    return this.length == 0;
  }

  public boolean isFull() {
    return this.length == this.array.length;
  }

}

/**
 * Your MyCircularQueue object will be instantiated and called as such:
 * MyCircularQueue obj = new MyCircularQueue(k);
 * boolean param_1 = obj.enQueue(value);
 * boolean param_2 = obj.deQueue();
 * int param_3 = obj.Front();
 * int param_4 = obj.Rear();
 * boolean param_5 = obj.isEmpty();
 * boolean param_6 = obj.isFull();
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/772999229/){:target="_blank"}

# 설명
1. 아래의 구조의 순환되는 Queue를 구현하는 문제이다.
- 생성자인 MyCircularQueue(k)는 Queue 크기인 k를 이용하여 객체를 초기화한다.
- 메서드인 Front()는 Queue의 앞에서 값을 가져오는 역할을 수행하며, 값이 없을 경우 -1을 반환한다.
- 메서드인 Rear()는 Queue의 뒤에서 값을 가져오는 역할을 수행하며, 값이 없을 경우 -1을 반환한다.
- 메서드인 enQueue(int value)는 Queue에 value를 추가하는 역할을 수행하며, 성공 시 true를 반환한다.
- 메서드인 deQueue()는 Queue의 값을 삭제하는 역할을 수행하며, 성공 시 true를 반환한다.
- 메서드인 isEmpty()는 Queue가 비어있는지 검증하는 역할을 수행한다.
- 메서드인 isFull()은 Queue가 꽉 차있는지 검증하는 역할을 수행한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- array는 Queue의 역할을 수행할 배열이다.
- front와 rear는 Queue의 앞과 뒤의 값을 저장할 변수이다.
- length는 Queue의 현재 크기를 저장할 변수이다.

3. 생성자인 MyCircularQueue(k)를 정의한다.
- Queue를 담당할 array를 k 크기의 정수 배열로 초기화한다.
- front와 rear는 0과 -1로, length는 0으로 초기화한다.

4. 메서드인 Front()를 정의한다.
- 8번에서 정의한 isEmpty() 메서드를 이용하여 Queue가 비어있는 경우 -1을, 비어있지 않으면 array의 front번째 값을 반환한다.

5. 메서드인 Rear()를 정의한다.
- 8번에서 정의한 isEmpty() 메서드를 이용하여 Queue가 비어있는 경우 -1을, 비어있지 않으면 array의 rear번째 값을 반환한다.

6. 메서드인 enQueue(int value)를 정의한다.
- 9번에서 정의한 isFull() 메서드를 이용하여 Queue가 꽉 차있지 않으면 아래를 수행한다.
  - rear에 Overflow를 방지하기 위해 $rear + 1$에서 array의 길이를 나눈 나머지 값을 넣어준다.
  - array의 rear번째 위치에 val을 넣어준다.
  - 값을 들어갔으므로 length를 증가시킨다.
  - 값을 Queue에서 성공적으로 추가했으므로 true를 반환한다.
- 위의 경우가 아니라면 false를 반환한다.

7. 메서드인 deQueue()를 정의한다.
- 9번에서 정의한 isFull() 메서드를 이용하여 Queue가 꽉 차있지 않으면 아래를 수행한다.
 - front에 Overflow를 방지하기 위해 $front + 1$에서 array의 길이를 나눈 나머지 값을 넣어준다.
 - 배열의 위치를 변경해서 시작 포인트를 뒤로 미뤘으므로, length를 감소시킨다.
 - 값을 Queue에서 성공적으로 제거했으므로 true를 반환한다.
- 위의 경우가 아니라면 false를 반환한다.

8. 메서드인 isEmpty()를 정의한다.
- length가 0인지를 검증한 결과를 반환한다.

9. 메서드인 isFull()을 정의한다.
- length와 array의 길이가 같은지 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignCircularQueue.java){:target="_blank"}에서 확인 가능합니다.