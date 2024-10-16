---
title: "Leetcode Java K-th Smallest in Lexicographical Order"
excerpt: "Leetcode K-th Smallest in Lexicographical Order Java 풀이"
last_modified_at: 2022-03-31T13:00:00
header:
  image: /assets/images/leetcode/k-th-smallest-in-lexicographical-order.png
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
[Link](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/){:target="_blank"}

# 코드
```java
class Solution {

  public int findKthNumber(int n, int k) {
    long cur = 1;
    while (k > 1) {
      long step = this.getStep(n, cur, cur + 1);
      if (step <= k - 1) {
        cur++;
        k -= step;
      } else {
        cur *= 10;
        k--;
      }
    }
    return (int) cur;
  }

  private long getStep(int n, long num1, long num2) {
    long count = 0;
    while (num1 <= n) {
      count += Math.min(n + 1, num2) - num1;
      num1 *= 10;
      num2 *= 10;
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/670742891/){:target="_blank"}

# 설명
1. 정수 n과 k가 주어지면 1 ~ n까지 숫자를 사전순 정렬을 수행했을 경우, k번째 값을 찾는 문제이다.

2. k번째 값을 담을 cur을 overflow를 방지하기 위해 long으로 정의하여, 1로 초기화한다.

3. k가 1 초과일 때까지 반복하여 탐색을 수행한다.
- step에 4번에서 정의한 getStep(int n, long num1, long num2) 메서드를 호출한 결과를 넣어준다.
- step이 $k - 1$ 이하인 경우, cur을 증가시키고 k에서 step만큼 빼준다.
- step이 $k - 1$ 초과인 경우, cur을 10배 증가시키고, k를 감소시킨다.

4. n에 근접한 값이 되기 위한 횟수를 계산하기 위한 getStep(int n, long num1, long num2) 메서드를 정의한다.
- 횟수를 계산할 step을 overflow를 방지하기 위해 long으로 정의하여, 0으로 초기화한다.
- num1이 n 이하일 때 까지 반복을 수행한다.
  - step에 $n + 1$과 num2 중 작은 값에서 num1을 뺀 값을 더해준다.
  - num1과 num2를 10배 증가시킨다.
- 반복이 완료되면 횟수를 저장한 step을 반환한다.

5. 반복이 완료되면 k번째 값인 cur을 int형으로 형 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KthSmallestInLexicographicalOrder.java){:target="_blank"}에서 확인 가능합니다.