---
title: "Leetcode Java Longest Binary Subsequence Less Than or Equal to K"
excerpt: "Leetcode - 'Longest Binary Subsequence Less Than or Equal to K' 문제 Java 풀이"
last_modified_at: 2025-06-26T17:50:00
header:
  image: /assets/images/leetcode/longest-binary-subsequence-less-than-or-equal-to-k.png
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
[Link](https://leetcode.com/problems/longest-binary-subsequence-less-than-or-equal-to-k/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestSubsequence(String s, int k) {
    char[] charArray = s.toCharArray();
    int result = 0;
    int cost = 1;
    for (int i = s.length() - 1; i >= 0; i--) {
      if (charArray[i] == '0' || cost <= k) {
        k -= cost * (charArray[i] - '0');
        result++;
      }
      if (cost <= k) {
        cost *= 2;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-all-k-distant-indices-in-an-array/submissions/1674760787/){:target="_blank"}

# 설명
1. k 이하의 이진수를 구성하는 문자열 s의 가장 긴 부분 배열의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray 는 문자열 s를 문자 배열로 변환한 변수이다.
- result는 부분 배열의 길이를 저장할 변수로, 0으로 초기화한다.
- cost는 이진수 값을 계산하기위한 변수로, 1로 초기화한다.

2. s의 마지막 위치에서 처음 위치까지 역순으로 i를 증가시키면서 아래를 반복한다.
- charArray[i] 문자가 0이거나 cost가 k 이하인 경우, k에 cost와 charArray[i]의 영문자 순서 값을 곱한 값을 빼주고 result를 증가시킨다.
- cost가 k 이하인 더 증가시킬 수 있는 경우, cost에 2를 곱해준다.

3. 반복이 완료되어 계산된 최대 길이인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestBinarySubsequenceLessThanOrEqualToK.java){:target="_blank"}에서 확인 가능합니다.