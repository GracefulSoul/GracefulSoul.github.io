---
title: "Leetcode Java Count Odd Numbers in an Interval Range"
excerpt: "Leetcode - 'Count Odd Numbers in an Interval Range' 문제 Java 풀이"
last_modified_at: 2025-12-07T16:50:00
header:
  image: /assets/images/leetcode/count-odd-numbers-in-an-interval-range.png
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
[Link](https://leetcode.com/problems/count-odd-numbers-in-an-interval-range/){:target="_blank"}

# 코드
```java
class Solution {

  public int countOdds(int low, int high) {
    return (high + 1) / 2 - low / 2;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-odd-numbers-in-an-interval-range/submissions/1849075283/){:target="_blank"}

# 설명
1. [low, high] 범위 내 홀수의 갯수를 구하는 문제이다.

2. 두 경우의 차분을 주어진 문제의 결과로 반환한다.
  - high 이하의 홀수 갯수인 $\frac{high + 1}{2}$개.
  - low 미만의 홀수 갯수인 $\frac{low}{2}$개.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountOddNumbersInAnIntervalRange.java){:target="_blank"}에서 확인 가능합니다.