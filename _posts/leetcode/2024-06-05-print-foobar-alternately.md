---
title: "Leetcode Java Print FooBar Alternately"
excerpt: "Leetcode Medium - 'Print FooBar Alternately' 문제 Java 풀이"
last_modified_at: 2024-06-05T20:10:00
header:
  image: /assets/images/leetcode/print-foobar-alternately.png
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
[Link](https://leetcode.com/problems/print-foobar-alternately/){:target="_blank"}

# 코드
```java
class FooBar {

  private int n;
  private Semaphore fooSemaphore;
  private Semaphore barSemaphore;

  public FooBar(int n) {
    this.n = n;
    this.fooSemaphore = new Semaphore(1);
    this.barSemaphore = new Semaphore(0);
  }

  public void foo(Runnable printFoo) throws InterruptedException {
    for (int i = 0; i < this.n; i++) {
      this.fooSemaphore.acquire();
      // printFoo.run() outputs "foo". Do not change or remove this line.
      printFoo.run();
      this.barSemaphore.release();
    }
  }

  public void bar(Runnable printBar) throws InterruptedException {
    for (int i = 0; i < this.n; i++) {
      this.barSemaphore.acquire();
      // printBar.run() outputs "bar". Do not change or remove this line.
      printBar.run();
      this.fooSemaphore.release();
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/print-foobar-alternately/submissions/1278413014/){:target="_blank"}

# 설명
1. 두 쓰레드 A와 B가 각자 "foo"를 출력하는 foo()와 "bar"를 출력하는 bar()를 수행할 때, "foobar"가 n번 출력되는 FooBar 클래스를 완성하는 문제이다.

2. 출력에 필요한 전역 변수를 정의한다.
- n은 출력하는 횟수를 저장할 변수이다.
- fooSemaphore와 barSemaphore는 foo와 bar의 순차적인 출력을 위한 변수이다.

3. 생성자인 FooBar(int n)를 정의한다.
- 전역 변수인 n에 주어진 n을 넣어준다.
- 전역 변수인 fooSemaphore와 barSemaphore에 "foo" 출력 이후 "bar"를 순차적으로 출력하기 위해서, fooSemaphore의 permits를 1, barSemaphore를 0인 Semaphore 객체로 초기화한다.

4. 메서드인 foo(Runnable printFoo)를 정의한다.
- 0부터 n까지 i를 증가시키며, 아래를 수행한다.
  - fooSemaphore를 잠금하여, 해당 순서 다음 "foo" 출력을 차단한다.
  - printFoo를 수행 후 barSemaphore를 잠금 해제하여 다음 순서에 "bar"를 출력할 수 있게 한다.

5. 메서드인 bar(Runnable printBar)를 정의한다.
- 0부터 n까지 i를 증가시키며, 아래를 수행한다.
  - barSemaphore를 잠금하여, 해당 순서 다음 "bar" 출력을 차단한다.
  - printBar를 수행 후 fooSemaphore를 잠금 해제하여 다음 순서에 "foo"를 출력할 수 있게 한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PrintFooBarAlternately.java){:target="_blank"}에서 확인 가능합니다.