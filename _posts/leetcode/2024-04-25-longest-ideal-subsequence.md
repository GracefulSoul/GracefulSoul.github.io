---
title: "Leetcode Java Longest Ideal Subsequence"
excerpt: "Leetcode Longest Ideal Subsequence Java"
last_modified_at: 2024-04-25T18:30:00
header:
  image: /assets/images/leetcode/longest-ideal-subsequence.png
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
[Link](https://leetcode.com/problems/longest-ideal-subsequence/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestIdealString(String s, int k) {
    int[] dp = new int[26];
    int result = 1;
    for (char c : s.toCharArray()) {
      int i = c - 'a';
      dp[i]++;
      for (int j = Math.max(0, i - k); j <= Math.min(25, i + k); j++) {
        if (i != j) {
          dp[i] = Math.max(dp[i], dp[j] + 1);
        }
      }
      result = Math.max(result, dp[i]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-ideal-subsequence/submissions/1241538282/){:target="_blank"}

# 설명
1. 아래 조건을 만족하는 문자열의 최대 길이를 반환하는 문제이다.
- 결과 문자열 t는 s의 부분 수열이다.
- t와 인접한 문자열의 알파벳 순서 차이는 k보다 작거나 같다.
- a와 z의 차잇값은 25로, 영문자는 순서 그대로에 대한 차잇값을 계산한다. 

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 최대 길이 계산에 필요한 변수로, 26 크기의 정수 배열로 초기화한다.
- result는 최대 길이를 계산할 변수로, 최소 길이인 1로 초기화한다.

3. s의 문자들을 순차적으로 c에 넣어 아래를 수행한다.
- i는 c의 영문자 순서를 넣어주고, dp[i]의 값을 증가시킨다.
- 0과 $i - k$ 중 큰 값부터 25와 $i + k$ 중 작은 값 이하까지 j를 증가시키면서 아래를 반복한다.
  - i와 j의 값이 다른 동일 문자가 아닌 경우, dp[i]에 dp[i]와 $dp[j] + 1$ 중 큰 값을 넣어준다.
- 위의 반복이 완료되면 result에 이전까지 최대 길이인 result와 현재 최대 길이인 dp[i]의 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestIdealSubsequence.java){:target="_blank"}에서 확인 가능합니다.