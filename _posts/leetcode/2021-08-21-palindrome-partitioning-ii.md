---
title: "Leetcode Java Palindrome Partitioning II"
excerpt: "Leetcode Palindrome Partitioning II Java 풀이"
last_modified_at: 2021-08-21T13:00:00
header:
  image: /assets/images/leetcode/palindrome-partitioning-ii.png
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
[Link](https://leetcode.com/problems/palindrome-partitioning-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int minCut(String s) {
    boolean dp[][] = new boolean[s.length() + 1][s.length() + 1];
    int min[] = new int[s.length()];
    for (int i = 0; i < s.length(); i++) {
      min[i] = i;
      for (int j = 0; j <= i; j++) {
        if (s.charAt(i) == s.charAt(j) && (j + 1 > i - 1 || dp[j + 1][i - 1])) {
          dp[j][i] = true;
          min[i] = j == 0 ? 0 : Math.min(min[i], min[j - 1] + 1);
        }
      }
    }
    return min[s.length() - 1];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/541704225/){:target="_blank"}

# 설명
1. 이전의 [Palindrome Partitioning](../palindrome-partitioning){:target="_blank"}과 유사한 문제로, 주어진 문자열 s를 앞뒤로 읽어도 같은 문자열(이하 회문)의 조합으로 자르기 위한 최소 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- DP를 저장할 dp를 2차원 boolean 배열의 $s.legnth() + 1 \times s.length() + 1$ 크기로 정의한다.
- 최소 횟수를 저장할 정수 배열인 min을 s.length() 크기로 정의한다.

3. 문자열 s의 처음부터 길이만큼 반복하여 회문의 조합으로 자르기 위한 최소 횟수를 구한다.
- min[i]에 i값을 기본값 으로 넣어준다.

4. 다시 문자열 s의 처음부터 i까지 반복하여준다.
- 문자열 s의 i번째 문자와 j번째 문자가 동일하고, $j + 1$이 $i - 1$보다 크거나 dp[$j + 1$][$i - 1$]의 값이 true 일 경우 아래를 수행한다.
  - dp[j][i]에 true를 넣어준다.
  - min[i]에 j가 0일 경우 0을, 그렇지 않은 경우 min[i]와 min[j - 1] + 1 중 작은 값을 넣어준다.

5. 반복이 완료되면 회문의 조합으로 자르기 위한 최소 횟수를 저장한 배열 min의 마지막 값인 min[$s.length() - 1$]을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PalindromePartitioningII.java){:target="_blank"}에서 확인 가능합니다.