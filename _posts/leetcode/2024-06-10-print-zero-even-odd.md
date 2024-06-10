---
title: "Leetcode Java Print Zero Even Odd"
excerpt: "Leetcode Print Zero Even Odd Java"
last_modified_at: 2024-06-10T18:50:00
header:
  image: /assets/images/leetcode/print-zero-even-odd.png
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
[Link](https://leetcode.com/problems/print-zero-even-odd/){:target="_blank"}

# 코드
```java
class ZeroEvenOdd {

  private int n;
  private Semaphore zeroSemaphore;
  private Semaphore evenSemaphore;
  private Semaphore oddSemaphore;

  public ZeroEvenOdd(int n) {
    this.n = n;
    this.zeroSemaphore = new Semaphore(1);
    this.evenSemaphore = new Semaphore(0);
    this.oddSemaphore = new Semaphore(0);
  }

  // printNumber.accept(x) outputs "x", where x is an integer.
  public void zero(IntConsumer printNumber) throws InterruptedException {
    for (int i = 1; i <= this.n; i++) {
      this.zeroSemaphore.acquire();
      printNumber.accept(0);
      if (i % 2 == 0) {
        this.evenSemaphore.release();
      } else {
        this.oddSemaphore.release();
      }
    }
  }

  public void even(IntConsumer printNumber) throws InterruptedException {
    for (int i = 2; i <= this.n; i += 2) {
      this.evenSemaphore.acquire();
      printNumber.accept(i);
      this.zeroSemaphore.release();
    }
  }

  public void odd(IntConsumer printNumber) throws InterruptedException {
    for (int i = 1; i <= this.n; i += 2) {
      this.oddSemaphore.acquire();
      printNumber.accept(i);
      this.zeroSemaphore.release();
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/print-zero-even-odd/submissions/1283666265/){:target="_blank"}

# 설명
1. 세 개의 쓰레드가 각각 0을 출력하는 zero, 홀수를 출력하는 odd, 짝수를 출력하는 even 메서드를 비동기로 호출할 때, n까지 0 출력 이후 홀수와 짝수를 순차적으로 출력하는 문제이다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- n은 출력되는 최대값을 저장할 변수이다.
- zeroSemaphore, evenSemaphore, oddSemaphore은 순차적으로 0과 짝수, 홀수를 출력하기 위한 순서를 제어하기 위한 변수이다.

3. 생성자인 ZeroEvenOdd(int n)를 정의한다.
- n을 전역 변수 n에 넣어준다.
- zeroSemaphore는 permits를 1로, evenSemaphore와 oddSemaphore는 0인 Semaphore 객체로 초기화한다.

4. 메서드인 zero(IntConsumer printNumber)를 정의한다.
- 10부터 n 이하까지 i를 증가시키며 아래를 반복한다.
  - zeroSemaphore를 잠궈준다.
  - printNumber를 0으로 수행하여, 0을 출력해준다.
  - i가 짝수이면 evenSemaphore를, 홀수이면 oddSemaphore를 release하여 잠금을 해제해준다.

5. 메서드인 even(IntConsumer printNumber)을 정의한다.
- 2부터 n 이하까지 i를 2씩 증가시키며 아래를 반복한다.
  - evenSemaphore를 잠금 후 printNumber를 i로 수행하여, i를 출력해준다.
  - zeroSemaphore를 release하여 잠금을 해제하여 다음 수행을 진행하게 해준다.

6. 메서드인 odd(IntConsumer printNumber)를 정의한다.
- 1부터 n 이하까지 i를 2씩 증가시키며 아래를 반복한다.
  - oddSemaphore를 잠금 후 printNumber를 i로 수행하여, i를 출력해준다.
  - zeroSemaphore를 release하여 잠금을 해제하여 다음 수행을 진행하게 해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PrintZeroEvenOdd.java){:target="_blank"}에서 확인 가능합니다.