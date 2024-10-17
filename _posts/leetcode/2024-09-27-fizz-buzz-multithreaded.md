---
title: "Leetcode Java Fizz Buzz Multithreaded"
excerpt: "Leetcode Medium - 'Fizz Buzz Multithreaded' 문제 Java 풀이"
last_modified_at: 2024-09-27T18:30:00
header:
  image: /assets/images/leetcode/fizz-buzz-multithreaded.png
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
[Link](https://leetcode.com/problems/fizz-buzz-multithreaded/){:target="_blank"}

# 코드
```java
class FizzBuzz {

  private int n;
  private int count = 1;

  public FizzBuzz(int n) {
    this.n = n;
  }

  // printFizz.run() outputs "fizz".
  public synchronized void fizz(Runnable printFizz) throws InterruptedException {
    while (this.count <= this.n) {
      if (this.count % 3 != 0 || this.count % 5 == 0) {
        wait();
        continue;
      }
      printFizz.run();
      this.count++;
      notifyAll();
    }
  }

  // printBuzz.run() outputs "buzz".
  public synchronized void buzz(Runnable printBuzz) throws InterruptedException {
    while (this.count <= this.n) {
      if (this.count % 5 != 0 || this.count % 3 == 0) {
        wait();
        continue;
      }
      printBuzz.run();
      this.count++;
      notifyAll();
    }
  }

  // printFizzBuzz.run() outputs "fizzbuzz".
  public synchronized void fizzbuzz(Runnable printFizzBuzz) throws InterruptedException {
    while (this.count <= this.n) {
      if (this.count % 15 != 0) {
        wait();
        continue;
      }
      printFizzBuzz.run();
      this.count++;
      notifyAll();
    }
  }

  // printNumber.accept(x) outputs "x", where x is an integer.
  public synchronized void number(IntConsumer printNumber) throws InterruptedException {
    while (this.count <= this.n) {
      if (this.count % 3 == 0 || this.count % 5 == 0) {
        wait();
        continue;
      }
      printNumber.accept(this.count);
      this.count++;
      notifyAll();
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/fizz-buzz-multithreaded/submissions/1403783246/){:target="_blank"}

# 설명
1. 아래의 규칙대로 [1, n] 범위 내에서 "fizz", "buzz", "fizzbuzz", 위치 값을 찍는 FizzBuzz 객체를 완성하는 문제이다.
- 생성자인 FizzBuzz(int n)는 n까지 각 값들을 출력하기 위한 객체를 초기화한다.
- 메서드인 fizz(printFizz)는 3의 배수이면서 5의 배수가 아닌 경우, printFizz를 호출하여 "fizz"를 출력한다.
- 메서드인 buzz(printBuzz)는 5의 배수이면서 3의 배수가 아닌 경우, printBuzz를 호출하여 "buzz"를 출력한다.
- 메서드인 fizzbuzz(printFizzBuzz)는 3과 5의 배수인 경우, printFizzBuzz를 호출하여 "fizzbuzz"를 출력한다.
- 메서드인 number(printNumber)는 3과 5의 배수가 아닌 경우, printnumber를 호출하여 현재 위치 값을 출력한다.

2. 순차적인 출력을 위한 전역 변수들을 정의한다.
- n은 생성자를 통해 주입된 출력의 상한 값을 저장한다.
- count는 현재 번호를 저장할 변수이다.

3. 생성자인 FizzBuzz(int n)를 완성한다.
- 전역 변수인 n에 전달된 n을 저장한다.
- 전역 변수인 count를 시작 숫자인 1로 초기화한다.

4. 메서드인 fizz(printFizz)를 완성한다.
- 하나의 쓰레드만 접근 가능하도록 synchronized 키워드를 추가한다.
- count가 n 이하일 때 까지 아래를 반복한다.
  - count가 3의 배수가 아니거나 5의 배수인 경우, 현재 쓰레드를 일시 중지시키고 다음 반복을 수행한다.
  - printFizz를 수행하여 "fizz"를 출력하고, count인 번호를 증가시킨다.
  - 현재 일시 중지된 모든 쓰레드를 깨운다.

5. 메서드인 buzz(printBuzz)를 완성한다.
- 하나의 쓰레드만 접근 가능하도록 synchronized 키워드를 추가한다.
- count가 n 이하일 때 까지 아래를 반복한다.
  - count가 3의 배수이거나 5의 배수가 아닌 경우, 현재 쓰레드를 일시 중지시키고 다음 반복을 수행한다.
  - printBuzz를 수행하여 "buzz"를 출력하고, count인 번호를 증가시킨다.
  - 현재 일시 중지된 모든 쓰레드를 깨운다.

6. 메서드인 fizzbuzz(printFizzBuzz)를 완성한다.
- 하나의 쓰레드만 접근 가능하도록 synchronized 키워드를 추가한다.
- count가 n 이하일 때 까지 아래를 반복한다.
  - count가 15의 배수가 아닌 경우, 현재 쓰레드를 일시 중지시키고 다음 반복을 수행한다.
  - printFizzBuzz를 수행하여 "fizzbuzz"를 출력하고, count인 번호를 증가시킨다.
  - 현재 일시 중지된 모든 쓰레드를 깨운다.

7. 메서드인 number(printNumber)를 완성한다.
- 하나의 쓰레드만 접근 가능하도록 synchronized 키워드를 추가한다.
- count가 n 이하일 때 까지 아래를 반복한다.
  - count가 3의 배수이거나 5의 배수인 경우, 현재 쓰레드를 일시 중지시키고 다음 반복을 수행한다.
  - printNumber를 수행하여 현재 번호를 출력하고, count인 번호를 증가시킨다.
  - 현재 일시 중지된 모든 쓰레드를 깨운다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FizzBuzzMultithreaded.java){:target="_blank"}에서 확인 가능합니다.