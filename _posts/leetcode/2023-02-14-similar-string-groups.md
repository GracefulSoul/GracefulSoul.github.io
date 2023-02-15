---
title: "Leetcode Java Similar String Groups"
excerpt: "Leetcode Similar String Groups Java"
last_modified_at: 2023-02-14T19:00:00
header:
  image: /assets/images/leetcode/similar-string-groups.png
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
[Link](https://leetcode.com/problems/similar-string-groups){:target="_blank"}

# 코드
```java
class Solution {

  public int numSimilarGroups(String[] strs) {
    boolean[] visited = new boolean[strs.length];
    int result = 0;
    for (int i = 0; i < strs.length; i++) {
      if (!visited[i]) {
        this.dfs(strs, i, visited);
        result++;
      }
    }
    return result;
  }

  private void dfs(String[] strs, int index, boolean[] visited) {
    visited[index] = true;
    for (int i = 0; i < strs.length; i++) {
      if (!visited[i] && this.isSimilar(strs[index], strs[i])) {
        this.dfs(strs, i, visited);
      }
    }
  }

  private boolean isSimilar(String s1, String s2) {
    int count = 0;
    for (int i = 0; i < s1.length(); i++) {
      if (s1.charAt(i) != s2.charAt(i)) {
        count++;
      }
      if (count > 2) {
        return false;
      }
    }
    return count == 0 || count == 2;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/similar-string-groups/submissions/897770384/){:target="_blank"}

# 설명
1. strs 내 아나그램으로 두 글자까지 변경하여 동일한 글자로 만들 수 있는 문자열 그룹의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- visited는 strs의 각 문자열 별 검증하기위해 방문한 이력을 남기기 위한 배열로, strs의 길이의 부울 배열로 초기화한다.
- result는 그룹의 수를 계산하기 위한 변수로, 0으로 초기화한다.

3. 0부터 strs의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- visited의 i번째 값이 false인 검증하지 않은 문자열이면 4번에서 정의한 dfs(String[] strs, int index, boolean[] visited) 메서드를 수행하고, result를 증가시킨다.

4. DFS 방식으로 동일 집단 검증을 수행할 dfs(String[] strs, int index, boolean[] visited) 메서드를 정의한다.
- visited의 index번째 값을 true로 바꾸어준다.
- 0부터 strs의 길이 미만까지 i를 증가시키며 아래를 수행한다.
  - visited의 i번째 값이 false인 검증하지 않은 문자열이면서 5번에서 정의한 isSimilar(String s1, String s2) 메서드를 수행하여 strs의 index번째 문자와 i번째 문자가 유사한 경우, index에 i를 넣어 재귀 호출을 수행한다.

5. 두 문자열이 유사한지 검증하기 위한 isSimilar(String s1, String s2) 메서드를 정의한다.
- count는 문자 변경에 대한 갯수를 세기 위한 변수로, 0으로 초기화한다.
- 0부터 s1의 길이 미만까지 i를 증가시키며 s1과 s2의 각 위치 별 다른 문자 갯수를 count에 저장하며, 2개를 넘으면 false를 반환한다.
- 반복이 완료되고 count가 0인 동일한 문자거나, 2인 두 문자의 위치를 변경했을 때 같은 문자가 되지를 검증한 결과를 반환한다.

6. 3번의 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SimilarStringGroups.java){:target="_blank"}에서 확인 가능합니다.