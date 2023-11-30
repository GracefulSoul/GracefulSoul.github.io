---
title: "Leetcode Java Pairs of Songs With Total Durations Divisible by 60"
excerpt: "Leetcode Pairs of Songs With Total Durations Divisible by 60 Java"
last_modified_at: 2023-11-29T20:20:00
header:
  image: /assets/images/leetcode/pairs-of-songs-with-total-durations-divisible-by-60.png
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
[Link](https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60){:target="_blank"}

# 코드
```java
class Solution {

  public int numPairsDivisibleBy60(int[] time) {
    long[] count = new long[60];
    for (int t : time) {
      count[t % 60]++;
    }
    long result = 0;
    if (count[0] > 1) {
      result += count[0] * (count[0] - 1) / 2;
    }
    if (count[30] > 1) {
      result += count[30] * (count[30] - 1) / 2;
    }
    for (int i = 1; i < 30; i++) {
      result += count[i] * count[60 - i];
    }
    return (int) result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/submissions/1108837055/){:target="_blank"}

# 설명
1. time 내 값들을 이용하여 두 값의 합이 60초 단위가 되는 경우의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 60초로 나눈 나머지 여분의 시간으로 끝나는 값들의 갯수를 저장할 변수로, overflow를 방지하기 위하여 long 형태의 배열로 초기화하고 time의 각 값들을 60으로 나눈 나머지의 위치에 갯수를 저장해준다.
- result 경우의 수를 저장할 변수로, overflow를 방지하기 위하여 long 형태의 0으로 초기화한다.

3. count[0]의 갯수가 2개 이상인 경우, 해당 값들의 순서를 변경했을 때 나올 수 있는 경우의 수인 $\frac{count[0] \times (count[0] - 1)}{2}$를 result에 더해준다.

4. 3. count[30]의 갯수가 2개 이상인 경우, 0초와 동일하게 해당 값들의 순서를 변경했을 때 나올 수 있는 경우의 수인 $\frac{count[30] \times (count[30] - 1)}{2}$를 result에 더해준다.

5. 0초와 30초를 제외한 1 ~ 29초 구간을 i를 증가시키며 60초 단위로 떨어지는 조합의 경우의 수를 result에 더해준 후, int로 형변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PairsOfSongsWithTotalDurationsDivisibleBy60.java){:target="_blank"}에서 확인 가능합니다.