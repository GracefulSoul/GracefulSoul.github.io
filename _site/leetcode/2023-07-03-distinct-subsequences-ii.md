---
title: "Leetcode Java Distinct Subsequences II"
excerpt: "Leetcode Distinct Subsequences II Java"
last_modified_at: 2023-07-03T19:20:00
header:
  image: /assets/images/leetcode/distinct-subsequences-ii.png
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
[Link](https://leetcode.com/problems/distinct-subsequences-ii){:target="_blank"}

# 코드
```java
class Solution {

  public int distinctSubseqII(String s) {
    int sum = 0;
    int[] count = new int[26];
    int mod = 1000000007;
    for (char c : s.toCharArray()) {
      int index = c - 'a';
      int curr = (sum + 1 - count[index] + mod) % mod;
      sum = (sum + curr) % mod;
      count[index] = (count[index] + curr) % mod;
    }
    return sum;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/distinct-subsequences-ii/submissions/985208040/){:target="_blank"}

# 설명
1. s의 비어있지 않은 고유 부분 수열의 수를 반환하는 문제이다.
- 고유 부분 수열은 일부 문자를 삭제하여 새로 만들 수 있는 문자열이다.
- 단, 답이 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용해 계산한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 고유 부분 수열의 수를 저장할 변수로, 0으로 초기화한다.
- count는 해당 문자열까지 부분 수열을 계산하기 위한 배열로, 알파벳의 수인 26 크기의 정수 배열로 초기화한다.
- mod는 모듈러를 적용할 변수로, $10^9 +7$로 초기화한다.

3. s의 모든 문자를 c에 순차적으로 넣어 아래를 반복한다.
- index에 c의 알파벳 순번을 넣어준다.
- curr은 현재 위치에서 고유 부분 수열의 수를 저장할 변수로, $sum + 1 - count[index]$에 mod를 더한 후 mod를 나눈 나머지를 넣어준다.
- sum에 sum과 curr을 더한 값을 mod로 나누어 넣어준다.
- count의 index번째 위치에 해당 값과 curr을 더한 값을 mod로 나누어 저장하고 다음 반복을 수행한다.

4. 반복이 완료되면 sum을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DistinctSubsequencesII.java){:target="_blank"}에서 확인 가능합니다.