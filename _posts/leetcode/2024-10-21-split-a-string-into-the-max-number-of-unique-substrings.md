---
title: "Leetcode Java Split a String Into the Max Number of Unique Substrings"
excerpt: "Leetcode - 'Split a String Into the Max Number of Unique Substrings' 문제 Java 풀이"
last_modified_at: 2024-10-21T17:30:00
header:
  image: /assets/images/leetcode/split-a-string-into-the-max-number-of-unique-substrings.png
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
[Link](https://leetcode.com/problems/split-a-string-into-the-max-number-of-unique-substrings/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxUniqueSplit(String s) {
    return this.dfs(s, 0, new HashSet<>());
  }

  private int dfs(String s, int i, Set<String> seen) {
    if (i == s.length()) {
      return 0;
    } else {
      int max = 0;
      for (int end = i + 1; end <= s.length(); end++) {
        String substring = s.substring(i, end);
        if (!seen.contains(substring)) {
          seen.add(substring);
          max = Math.max(max, 1 + this.dfs(s, end, seen));
          seen.remove(substring);
        }
      }
      return max;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-kth-bit-in-nth-binary-string/submissions/1426923165/){:target="_blank"}

# 설명
1. s를 이용하여 연속된 문자들을 고유한 문자열의 부분 배열로 나눌 때, 가능한 최대 갯수를 계산하는 문제이다.

2. 3번에서 정의한 dfs(String s, int i, Set<String> seen) 메서드를 i에 0, seen에 새 HashSet을 초기화하여 넣어 수행한 결과를 반환한다.

3. DFS 방식으로 부분 문자열의 갯수를 계산할 dfs(String s, int i, Set<String> seen) 메서드를 정의한다.
- i가 s의 길이와 동일한 마지막 문자인 경우, 0을 반환한다.
- 위의 경우가 아니라면 아래를 수행한다.
  - max는 부분 배열의 갯수를 계산할 변수로, 0으로 초기화한다.
  - $i + 1$부터 s의 길이 이하까지 end를 증가시키며 s의 [i, end] 사이의 문자열이 seen에 포함되지 않은 경우, 다음을 수행한다.
  - seen에 해당 문자열을 넣고, max에 i의 자리에 end를 넣고 재귀 호출한 결과에 현재 경우인 1을 더한 값 중 큰 값을 넣어준 후 넣은 문자열을 다시 제거하여 다음 반복을 재개한다.
- 위의 반복으로 계산된 max를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindKthBitInNthBinaryString.java){:target="_blank"}에서 확인 가능합니다.