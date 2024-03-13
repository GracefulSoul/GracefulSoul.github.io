---
title: "Leetcode Java Find the Pivot Integer"
excerpt: "Leetcode Find the Pivot Integer Java"
last_modified_at: 2024-03-13T19:10:00
header:
  image: /assets/images/leetcode/find-the-pivot-integer.png
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
[Link](https://leetcode.com/problems/find-the-pivot-integer){:target="_blank"}

# 코드
```java
class Solution {

  public int pivotInteger(int n) {
    for (int i = 0, j = n, sum = 0; i < j;) {
      if (sum > 0) {
        sum -= j--;
      } else {
        sum += i++;
      }
      if (sum == 0 && i == j) {
        return i;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-pivot-integer/submissions/1202416570/){:target="_blank"}

# 설명
1. 1부터 x까지, x부터 n까지 합이 동일한 x를 찾는 문제이다.
- x가 존재하지 않으면, -1을 주어진 문제의 결과로 반환한다.

2. i와 sum은 0, j는 n으로초기화하여 i가 j 미만일 때 까지 아래를 반복한다.
- sum이 0보다 큰 경우, sum에 j를 빼주고 j를 감소시킨다.
- sum이 0보다 작거나 같은 경우, sum에 i를 더해주고 i를 증가시킨다.
- sum이 0이면서 i와 j가 동일한 경우, i를 주어진 문제의 결과로 반환한다.

3. 반복이 완료되면 x가 존재하지 않으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindThePivotInteger.java){:target="_blank"}에서 확인 가능합니다.