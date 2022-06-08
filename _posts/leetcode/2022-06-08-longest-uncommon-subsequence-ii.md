---
title: "Leetcode Java Longest Uncommon Subsequence II"
excerpt: "Leetcode Longest Uncommon Subsequence II Java"
last_modified_at: 2022-06-08T21:00:00
header:
  image: /assets/images/leetcode/longest-uncommon-subsequence-ii.png
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
[Link](https://leetcode.com/problems/longest-uncommon-subsequence-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int findLUSlength(String[] strs) {
    int result = -1;
    int length = strs.length;
    for (int i = 0; i < length; i++) {
      if (strs[i].length() < result) {
        continue;
      }
      int j = -1;
      while (++j < length) {
        if (i != j && this.isSubsequence(strs[i], strs[j])) {
          break;
        }
      }
      if (j == length) {
        result = Math.max(result, strs[i].length());
      }
    }
    return result;
  }

  private boolean isSubsequence(String s1, String s2) {
    int i = 0;
    int j = 0;
    while (i < s1.length() && j < s2.length()) {
      if (s1.charAt(i) == s2.charAt(j++)) {
        i++;
      }
    }
    return i == s1.length();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/717257423/){:target="_blank"}

# 설명
1. 이전 [Longest Uncommon Subsequence I](../longest-uncommon-subsequence-i){:target="_blank"}와 유사한 문제로, strs 배열 내 문자열들 중 유일한 가장 긴 [부분 수열](https://en.wikipedia.org/wiki/Subsequence){:target="_blank"} 문자열의 길이를 구하는 문제로, 유일한 부분 수열 문자열이 존재하지 않으면 -1을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 strs 배열 내 문자열들 중 유일한 가장 긴 부분 수열 문자열의 길이를 저장할 변수로, 존재하지 않을 경우의 값인 -1로 초기화한다.
- length는 strs 배열의 크기를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키며 반복을 수행한다.
- strs의 i번째 문자열의 길이가 result보다 작은 경우, 탐색할 의미가 없으므로 다음 반복을 수행한다.
- j를 -1로 초기화 하여 length보다 작을 때 까지 j를 증가시키며, i와 j가 같지 않고 4번에서 정의한 isSubsequence(String s1, String s2) 메서드를 이용하여 i번째 문자열이 j번째 문자열의 부분 수열이면 반복을 중지한다.
- j가 length와 동일한 경우 마지막 문자열까지 탐색하였으므로, result에 result와 i번째 문자열의 길이 중 큰 값을 넣어준다.

4. s1이 s2의 부분 수열인지를 검증하기 위한 isSubsequence(String s1, String s2) 메서드를 정의한다.
- i는 s1의 위치 값을, j는 s2의 위치 값을 나타낼 변수로 0으로 초기화한다.
- i가 s1 길이 미만이고, j가 s2 길이 미만일 때 까지 아래를 반복한다.
  - s1의 i번째 문자가 s2의 j번째 문자와 동일한지 검증하면서 j를 증가시키고, 동일한 경우에만 i를 증가시킨다.
- 반복이 완료되면 i와 s1의 길이가 동일한지 검증하여, s1이 s2의 부분 수열에 속하는지 결과를 반환한다.

5. 반복이 완료되면 strs 배열 내 문자열들 중 유일한 가장 긴 부분 수열 문자열의 길이를 저장할 변수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestUncommonSubsequenceII.java){:target="_blank"}에서 확인 가능합니다.