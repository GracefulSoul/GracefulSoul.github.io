---
title: "Leetcode Java Count Number of Teams"
excerpt: "Leetcode Count Number of Teams Java"
last_modified_at: 2024-07-29T18:10:00
header:
  image: /assets/images/leetcode/count-number-of-teams.png
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
[Link](https://leetcode.com/problems/count-number-of-teams/){:target="_blank"}

# 코드
```java
class Solution {

  public int numTeams(int[] rating) {
    int length = rating.length;
    int[][] dp = new int[length][2];
    int result = 0;
    for (int i = 1; i < length; i++) {
      for (int j = 0; j < i; j++) {
        if (rating[i] > rating[j]) {
          dp[i][0]++;
          result += dp[j][0];
        } else {
          dp[i][1]++;
          result += dp[j][1];
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-number-of-teams/submissions/1337081719/){:target="_blank"}

# 설명
1. 각 고유한 등급이 저장된 rating을 이용하여 아래의 규칙을 만족하는 팀의 갯수를 계산하는 문제이다.
- 한 팀은 세 병사로 구성된다.
- 0 <= i < j < k < n 의 세 값인 i, j, k는 $rating[i] < rating[j] < rating[k]$ 혹은 $rating[i] > rating[j] > rating[k]$을 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 rating의 길이로 저장한 변수이다.
- dp는 팀의 갯수를 계산하기 위해 사용할 배열로, $length \times 2$ 크기의 2차원 정수 배열로 초기화한다.
- result는 팀의 갯수를 저장할 변수로, 0으로 초기화한다.

3. 1부터 length 미만까지 i를 증가시키고, 0부터 i 미만까지 j를 증가시키며 아래를 수행한다.
- rating[i]가 rating[j]보다 큰 경우, 아래를 수행한다.
  - dp[i][0]을 증가시켜 i 위치 아래로 작은 값의 갯수를 증가시켜준다.
  - result에 rating[j]보다 작은 rating[k]가 가능한 갯수인 dp[j][0]의 값을 더해준다.
- rating[i]가 rating[j]보다 작은 경우, 아래를 수행한다.
  - dp[i][1]을 증가시켜 i 위치 아래로 큰 값의 갯수를 증가시켜준다.
  - result에 rating[j]보다 큰 rating[k]가 가능한 갯수인 dp[j][1]의 값을 더해준다.

4. 반복이 완료되면 가능한 팀의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountNumberOfTeams.java){:target="_blank"}에서 확인 가능합니다.