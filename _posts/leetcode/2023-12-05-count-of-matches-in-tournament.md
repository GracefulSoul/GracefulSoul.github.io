---
title: "Leetcode Java Count of Matches in Tournament"
excerpt: "Leetcode Count of Matches in Tournament Java"
last_modified_at: 2023-12-05T19:20:00
header:
  image: /assets/images/leetcode/count-of-matches-in-tournament.png
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
[Link](https://leetcode.com/problems/count-of-matches-in-tournament){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfMatches(int n) {
    return n - 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-of-matches-in-tournament/submissions/1112813048/){:target="_blank"}

# 설명
1. n개의 팀을 이용해서 토너먼트 수행하는 경우, 경기 숫자를 구하는 문제이다.

2. 토너먼트는 모든 경우에 아래와 같이 계산되므로, $n - 1$을 주어진 문제의 결과로 반환한다.
- 토너먼트의 기본 룰은 아래와 같다.
  - n이 짝수인 경우, $\frac{n}{2}$회 경기가 진행되고 동일한 값만큼의 팀이 다음 경기를 수행하게된다.
  - n이 홀수인 경우, 짝수와 동일한 횟수의 경기와 팀이 다음 라운드로 진출하지만 부전승으로 한 팀이 다음 경기에 합류하게 된다.
- 위를 통해 모든 경기는 진 팀만 토너먼트에서 탈락되므로, 우승한 한 팀만 남게되면 $n - 1$번의 경기를 수행해야한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/Largest3SameDigitNumberInString.java){:target="_blank"}에서 확인 가능합니다.