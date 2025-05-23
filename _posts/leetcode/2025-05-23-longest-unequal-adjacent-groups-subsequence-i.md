---
title: "Leetcode Java Longest Unequal Adjacent Groups Subsequence I"
excerpt: "Leetcode - 'Longest Unequal Adjacent Groups Subsequence I' 문제 Java 풀이"
last_modified_at: 2025-05-23T21:30:00
header:
  image: /assets/images/leetcode/longest-unequal-adjacent-groups-subsequence-i.png
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
[Link](https://leetcode.com/problems/longest-unequal-adjacent-groups-subsequence-i/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> getLongestSubsequence(String[] words, int[] groups) {
    List<String> result = new ArrayList<>();
    result.add(words[0]);
    for (int i = 1; i < words.length; i++) {
      if (groups[i - 1] != groups[i]) {
        result.add(words[i]);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-unequal-adjacent-groups-subsequence-i/submissions/1642128624/){:target="_blank"}

# 설명
1. 0과 1로 구성된 groups를 이용하여 그룹이 동일하지 않도록 동일한 위치의 words의 문자들을 구성하여 반환하는 문제이다.
- 답이 여러 개여도 임의 하나만 반환하면 된다.

2. result는 결과를 저장하기 위한 배열로, ArrayList로 초기화하여 words의 첫 문자를 넣어준다.

3. 1부터 words의 길이 미만까지 i를 증가시키며, groups의 $i - 1$번째 값과 i번째 값이 다른 다른 그룹이면 result에 words[i]를 넣어준다.

4. 반복이 완료되어 그룹이 다른 문자들을 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestUnequalAdjacentGroupsSubsequenceI.java){:target="_blank"}에서 확인 가능합니다.