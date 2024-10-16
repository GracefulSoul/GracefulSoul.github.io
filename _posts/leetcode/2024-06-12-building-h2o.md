---
title: "Leetcode Java Building H2O"
excerpt: "Leetcode Building H2O Java"
last_modified_at: 2024-06-12T18:20:00
header:
  image: /assets/images/leetcode/building-h2o.png
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
[Link](https://leetcode.com/problems/building-h2o/){:target="_blank"}

# 코드
```java
class H2O {

  private Semaphore hSemaphore;
  private Semaphore oSemaphore;

  public H2O() {
    this.hSemaphore = new Semaphore(2, true);
    this.oSemaphore = new Semaphore(0, true);
  }

  public void hydrogen(Runnable releaseHydrogen) throws InterruptedException {
    this.hSemaphore.acquire();
    // releaseHydrogen.run() outputs "H". Do not change or remove this line.
    releaseHydrogen.run();
    this.oSemaphore.release();
  }

  public void oxygen(Runnable releaseOxygen) throws InterruptedException {
    this.oSemaphore.acquire(2);
    // releaseOxygen.run() outputs "O". Do not change or remove this line.
    releaseOxygen.run();
    this.hSemaphore.release(2);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/building-h2o/submissions/1285804415/){:target="_blank"}

# 설명
1. 어떠한 순서대로 호출하더라도 물의 분자식인 "HHO"(H<sub>2</sub>O)를 출력하는 H2O 클래스를 완성하는 문제이다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- hSemaphore와 oSemaphore는 "H"문자와 "O" 문자를 분자식 순서로 출력하기 위해 제어할 변수이다.

3. 생성자인 H2O()를 정의한다.
- hSemaphore는 "H" 문자 출력 제어할 변수로, 2번의 잠금과 FIFO방식을 사용하는 Semaphore로 초기화한다.
- oSemaphore는 "O" 문자 출력 제어할 변수로, 1번의 잠금과 FIFO방식을 사용하는 Semaphore로 초기화한다.

4. 메서드인 hydrogen(Runnable releaseHydrogen)을 정의한다.
- hSemaphore를 첫 번째 잠금하고 releaseHydrogen를 수행한다.
- oSemaphore를 첫 번째 잠금 해제한다.

5. 메서드인 oxygen(Runnable releaseOxygen)을 정의한다.
- oSemaphore를 두 번째 잠금하고 releaseOxygen을 수행한다.
- hSemaphore를 두 번째 잠금 해제한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BuildingH2O.java){:target="_blank"}에서 확인 가능합니다.