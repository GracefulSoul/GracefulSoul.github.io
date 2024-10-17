---
title: "Leetcode Java Number of Music Playlists"
excerpt: "Leetcode - 'Number of Music Playlists' 문제 Java 풀이"
last_modified_at: 2023-05-08T10:20:00
header:
  image: /assets/images/leetcode/number-of-music-playlists.png
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
[Link](https://leetcode.com/problems/number-of-music-playlists){:target="_blank"}

# 코드
```java
class Solution {

  public int numMusicPlaylists(int n, int goal, int k) {
    int mod = 1000000007;
    long[][] dp = new long[goal + 1][n + 1];
    dp[0][0] = 1;
    for (int i = 1; i <= goal; i++) {
      for (int j = 1; j <= n; j++) {
        dp[i][j] = (dp[i - 1][j - 1] * (n - (j - 1))) % mod;
        if (j > k) {
          dp[i][j] = (dp[i][j] + (dp[i - 1][j] * (j - k)) % mod) % mod;
        }
      }
    }
    return (int) dp[goal][n];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-music-playlists/submissions/946603763/){:target="_blank"}

# 설명
1. n개의 서로 다른 노래를 이용하여 아래의 규칙을 만족하는 goal개의 노래로 이루어진 재생 목록을 만들 경우, 만들 수 있는 재생 목록의 수를 구하는 문제이다.
- 모든 노래는 최소 한 번 이상 재생된다.
- 이미 재생된 노래는 k개의 다른 노래들을 재생해야 다시 재생할 수 있다.
- 단, 재생 목록의 수가 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용해 계산한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- mod는 모듈러를 적용할 변수로, $10^9 +7$로 초기화한다.
- dp는 재생 목록의 수를 계산하기 위한 변수로, $(goal + 1) \times (n + 1)$ 크기의 숫자가 매우 클 수 있으므로 long 배열로 초기화하고 맨 처음 위치에 1을 넣어준다.

3. 1부터 goal 이하까지 i를 증가시키고, 1부터 n 이하까지 j를 증가시키며 아래를 수행한다.
- dp[i][j] 위치에 $dp[i - 1][j - 1] \times (n - (j - 1))$의 값을 mod로 나눈 나머지 값을 넣어준다.
- j가 k보다 큰 경우 k개의 다른 노래를 재생하여 재생된 곡을 다시 재생 가능하므로, dp[i - 1][j]의 경우의 수에 $j - k$를 곱한 값을 dp[i][j]에 각 단계 별로 mod를 나눈 나머지를 넣어준다.

4. 반복이 완료되면 모듈러 $10^9 + 7$을 적용하여 경우의 수를 구한 dp[goal][n]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfMusicPlaylists.java){:target="_blank"}에서 확인 가능합니다.