---
title: "Leetcode Java Find And Replace in String"
excerpt: "Leetcode Find And Replace in String Java"
last_modified_at: 2023-02-08T19:40:00
header:
  image: /assets/images/leetcode/find-and-replace-in-string.png
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
[Link](https://leetcode.com/problems/find-and-replace-in-string){:target="_blank"}

# 코드
```java
class Solution {

  public String findReplaceString(String s, int[] indices, String[] sources, String[] targets) {
    int[] dp = new int[s.length()];
    for (int idx = 0; idx < indices.length; idx++) {
      if (s.startsWith(sources[idx], indices[idx])) {
        dp[indices[idx]] = idx + 1;
      }
    }
    StringBuilder sb = new StringBuilder();
    int index = 0;
    while (index < s.length()) {
      if (dp[index] > 0) {
        sb.append(targets[dp[index] - 1]);
        index += sources[dp[index] - 1].length();
      } else {
        sb.append(s.charAt(index++));
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-and-replace-in-string/submissions/893971229/){:target="_blank"}

# 설명
1. s에서 indices의 각 위치에서 sources로 시작하는지 검증하여 targets의 문자열로 변경하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- dp는 문자열 s의 각 시작 위치에 sources와 target의 위치 값을 저장할 배열로, s의 길이의 크기로 초기화하고 아래를 수행한다.
  - 0부터 indices의 길이 미만까지 idx를 증가시키며 s의 indices[idx]의 위치에서 sources[idx]의 문자열로 시작하는지 검증하여 dp의 indices[idx]번째 위치에 int의 초기값보다 크게 $idx + 1$을 넣어준다.
- sb는 결과 문자열을 저장할 변수로, StringBuilder로 초기화한다.
- index는 s의 위치 값을 저장할 변수로, 0으로 초기화한다.

3. index가 s의 길이 미만까지 아래를 반복한다.
- dp의 index번째 값이 1보다 큰 경우, sb에 targets의 $dp[index] - 1$번째 문자열을 넣어 변경된 문자열로 이어주고 index에 sources의 $dp[index] - 1$번째 문자열의 길이만큼 증가시켜 다음 위치로 이동시켜준다.
  - int의 초기값 0이고, 위치의 시작 지점이 0이므로 위치 변수를 1씩 증가시켰다가 사용할 때 1씩 감소시켜 사용하는 것이다.
- 위의 경우가 아니라면, sb에 s의 index번째 문자를 넣어 기존 문자로 이어주고 index를 증가시킨다.

4. 반복이 완료되면 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindAndReplaceInString.java){:target="_blank"}에서 확인 가능합니다.