---
title: "Leetcode Java Print in Order"
excerpt: "Leetcode Easy - 'Print in Order' 문제 Java 풀이"
last_modified_at: 2024-05-26T13:00:00
header:
  image: /assets/images/leetcode/print-in-order.png
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
[Link](https://leetcode.com/problems/print-in-order/){:target="_blank"}

# 코드
```java
class Foo {

  private Semaphore semaphore;

  public Foo() {
    this.semaphore = new Semaphore(0);
  }

  public void first(Runnable printFirst) throws InterruptedException {
    // printFirst.run() outputs "first". Do not change or remove this line.
    printFirst.run();
    this.semaphore.release();
  }

  public void second(Runnable printSecond) throws InterruptedException {
    while (!this.semaphore.tryAcquire(1));
    // printSecond.run() outputs "second". Do not change or remove this line.
    printSecond.run();
    this.semaphore.release(2);
  }

  public void third(Runnable printThird) throws InterruptedException {
    while (!this.semaphore.tryAcquire(2));
    // printThird.run() outputs "third". Do not change or remove this line.
    printThird.run();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/print-in-order/submissions/1268099185/){:target="_blank"}

# 설명
1. 어떠한 순서의 호출이어도 first, second, third를 순차적으로 출력하는 Foo 클래스를 완성하는 문제이다.
- 생성자인 Foo()는 객체를 초기화한다.
- 메서드인 first(Runnable printFirst), second(Runnable printSecond), third(Runnable printThird)는 각 호출에 대해 Runnable로 구현된 파라미터를 수행한다.

2. 전역 변수인 semaphore는 각 호출에 대한 잠금과 해제를 수행하기 위한 변수이다.

3. 생성자인 Foo()를 정의한다.
- semaphore에 신규 Semaphore 객체를 공유 자원을 0으로 생성하여 넣어준다.

4. 메서드인 first(Runnable printFirst)를 정의한다.
- printFirst을 수행하고 semaphore를 release하여 잠금 해제를 수행한다.

5. 메서드인 second(Runnable printSecond)를 정의한다.
- semaphore에 first 메서드가 release 될 때 까지 기다려 다음 수행을 대기한다.
- printSecond을 수행하고 semaphore에 permits를 2로 release하여 잠금 해제를 수행한다.

6. 메서드인 third(Runnable printThird)를 정의한다.
- semaphore에 second 메서드가 release 될 때 까지 기다려 다음 수행을 대기한다.
- printThird를 수행한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PrintInOrder.java){:target="_blank"}에서 확인 가능합니다.