---
title: "Leetcode Java Number of Recent Calls"
excerpt: "Leetcode Number of Recent Calls Java"
last_modified_at: 2023-06-16T20:10:00
header:
  image: /assets/images/leetcode/number-of-recent-calls.png
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
[Link](https://leetcode.com/problems/number-of-recent-calls){:target="_blank"}

# 코드
```java
class RecentCounter {

  private Deque<Integer> time;

  public RecentCounter() {
    this.time = new LinkedList<>();
  }

  public int ping(int t) {
    this.time.addLast(t);
    while (this.time.getFirst() < t - 3000) {
      this.time.removeFirst();
    }
    return this.time.size();
  }

}

/**
 * Your RecentCounter object will be instantiated and called as such:
 * RecentCounter obj = new RecentCounter();
 * int param_1 = obj.ping(t);
 */
```

# 결과
[Link](https://leetcode.com/problems/number-of-recent-calls/submissions/972543139/){:target="_blank"}

# 설명
1. 일정 시간 범위 내 최근 요청 수를 계산하는 RecentCounter 클래스를 완성하는 문제이다.
- 생성자인 RecentCounter()는 최근 요청이 0인 카운터를 초기화한다.
- 메서드인 ping(int t)은 시간 t를 새 요청으로 추가하고, 최근 3000 밀리초 내인 [$t - 3000$, t] 사이의 요청 횟수를 반환한다. 단, 모든 ping의 호출에 이전 호출보다 더 큰 t 값을 사용한다.

2. 최근 요청 수를 계산하기 위한 전역 변수를 정의한다.
- time은 최근 요청 시간을 저장할 변수이다.

3. 생성자인 RecentCounter()를 정의한다.
- time을 LinkedList로 초기화한다.

4. 메서드인 ping(int t)을 정의한다.
- time의 마지막에 t를 넣어준다.
- time의 앞의 값들 중 $t - 3000$보다 작은 값들은 모두 제거한다.
- 최근 3000 밀리초 내 요청 수가 저장된 time의 크기를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfRecentCalls.java){:target="_blank"}에서 확인 가능합니다.