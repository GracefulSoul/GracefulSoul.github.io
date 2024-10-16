---
title: "Leetcode Java Friends Of Appropriate Ages"
excerpt: "Leetcode Friends Of Appropriate Ages Java"
last_modified_at: 2023-02-01T20:20:00
header:
  image: /assets/images/leetcode/friends-of-appropriate-ages.png
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
[Link](https://leetcode.com/problems/friends-of-appropriate-ages){:target="_blank"}

# 코드
```java
class Solution {

  public int numFriendRequests(int[] ages) {
    int[] dp = new int[121];
    for (int age : ages) {
      dp[age]++;
    }
    for (int idx = 1; idx <= 120; idx++) {
      dp[idx] += dp[idx - 1];
    }
    int result = 0;
    for (int i = 120, j = 120; i >= 1; i--) {
      while (j > ((0.5 * i) + 7)) {
        j--;
      }
      if (++j <= i) {
        result += (dp[i] - dp[i - 1]) * (dp[i] - dp[j - 1] - 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/friends-of-appropriate-ages/submissions/889363899/){:target="_blank"}

# 설명
1. 동일하지 않은 x와 y에 대해서 아래의 조건을 모두 만족하지 않는 경우 친구 요청을 수행할 수 있는데, ages를 이용하여 해당 요청의 수를 구하는 문제이다.
- $ages[y] <= \frac{ages[x]}{2} + 7$
- $ages[y] > ages[x]$
- $ages[y] > 100$ && $ages[x] < 100$

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 친구 요청의 수를 계산하기 위한 배열로, 최대 나이인 120보다 큰 121의 크기로 초기화하고 아래를 수행한다.
  - dp 내 ages의 각 나이 값에 해당하는 위치 값을 증가시켜준다.
  - 1부터 120 이하까지 idx를 증가시키며 dp의 이전 값을 현재 위치의 값에 더해준다.
- result는 친구 요청의 수를 저장하기 위한 변수로, 0으로 초기화한다.

3. i와 j를 120부터 i가 1 이상일 때 까지 감소시키며 아래를 반복한다.
- j가 첫 번째 기본 조건인 $j <= \frac{i}{2} + 7$를 만족할 때 까지 j를 감소시켜준다.
- j를 증가시킨 후 해당 값이 i보다 큰 경우, result에 아래 두 수의 곱인 경우의 수를 더해준다.
  - dp의 i번째 값에서 $i - 1$번째 값의 차잇값인 해당 위치에 해당하는 친구들의 숫자.
  - dp의 i번째 값에서 $j - 1$번째 값과 1을 뺀 값을 곱한 친구 요청을 수행할 수 있는 친구들의 숫자.

4. 3번의 반복이 완료되면 친구 요청의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FriendsOfAppropriateAges.java){:target="_blank"}에서 확인 가능합니다.