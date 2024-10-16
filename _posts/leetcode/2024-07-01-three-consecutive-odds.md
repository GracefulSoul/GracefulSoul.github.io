---
title: "Leetcode Java Three Consecutive Odds"
excerpt: "Leetcode Three Consecutive Odds Java"
last_modified_at: 2024-07-01T17:40:00
header:
  image: /assets/images/leetcode/three-consecutive-odds.png
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
[Link](https://leetcode.com/problems/three-consecutive-odds/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean threeConsecutiveOdds(int[] arr) {
    for (int i = 0, count = 0; i < arr.length; i++) {
      if (arr[i] % 2 == 0) {
        count = 0;
      } else if (++count == 3) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/three-consecutive-odds/submissions/1305629620/){:target="_blank"}

# 설명
1. arr 내 연속된 값들 중 홀수가 3개 연달아 존재하는지 검증하는 문제이다.

2. count는 연속된 홀수의 갯수를 계산할 변수로 0으로, 0부터 arr의 길이 미만까지 i를 증가시키면서 아래를 반복한다.
- arr[i]의 값을 짝수이면, count를 0으로 초기화한다.
- arr[i]의 값이 홀수이면, count를 증가시키고 해당 값이 3이면 true를 주어진 문제의 결과로 반환한다.

3. 반복이 완료되면 arr 내 연속된 값들 중 홀수가 3개 연달아 있지 않으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ThreeConsecutiveOdds.java){:target="_blank"}에서 확인 가능합니다.