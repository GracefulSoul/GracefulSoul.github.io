---
title: "Leetcode Java Freedom Trail"
excerpt: "Leetcode Freedom Trail Java"
last_modified_at: 2022-05-30T18:00:00
header:
  image: /assets/images/leetcode/freedom-trail.png
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
[Link](https://leetcode.com/problems/freedom-trail/){:target="_blank"}

# 코드
```java
class Solution {

  public int findRotateSteps(String ring, String key) {
    int length = ring.length();
    List<Integer>[] position = new ArrayList[26];
    int[][] dp = new int[length][key.length()];
    for (int idx = 0; idx < 26; idx++) {
      position[idx] = new ArrayList<>();
    }
    for (int idx = 0; idx < length; idx++) {
      position[ring.charAt(idx) - 'a'].add(idx);
    }
    return this.dfs(position, dp, ring, length, key, 0, 0);
  }

  private int dfs(List<Integer>[] position, int[][] dp, String ring, int length, String key, int x, int y) {
    if (y == key.length()) {
      return 0;
    } else if (dp[x][y] != 0) {
      return dp[x][y];
    } else {
      int result = Integer.MAX_VALUE;
      for (int num : position[key.charAt(y) - 'a']) {
        int diff = Math.abs(x - num);
        result = Math.min(result, Math.min(diff, length - diff) + this.dfs(position, dp, ring, length, key, num, y + 1));
      }
      dp[x][y] = result + 1;
      return result + 1;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/710333262/){:target="_blank"}

# 설명
1. ring에 포함된 문자를 다어얼 형태로 배치하여 key에 해당하는 단어를 만들기 위한 최소 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 ring의 길이를 저장할 변수이다.
- position은 ring에 포함된 단어의 위치 값을 저장하기 위한 변수로, 알파벳 크기인 26의 ArrayList 배열로 정의한다.
- dp는 경우의 수를 저장하기 위한 변수로, length와 key의 길이 크기인 2차원 배열로 정의한다.

3. position에 ArrayList를 초기화하여 넣어주고, ring의 모든 문자의 위치 값을 position 내 해당 알파벳 위치값에 해당하는 ArrayList에 넣어준다.

4. 5번에서 정의한 dfs(List<Integer>[] position, int[][] dp, String ring, int length, String key, int x, int y) 메서드를 수행한 결과를 주어진 문제의 결과로 반환한다.

5. DFS 방식으로 문제를 탐색할 dfs(List<Integer>[] position, int[][] dp, String ring, int length, String key, int x, int y) 메서드를 정의한다.
- y가 key의 length와 동일한 경우, 해당 값이 존재하지 않으므로 0을 반환한다.
- dp[x][y] 값이 0이 아닌 경우, 이미 탐색된 위치의 값이므로 dp[x][y]의 값을 반환한다.
- result에 정수의 최댓값을 넣어준다.
- key의 y번째 문자에 해당하는 ArrayList를 position에서 꺼내 각 값을 num으로 아래를 수행한다.
  - diff에 x와 num의 차이의 절대값을 넣어준다.
  - result에 diff와 $length - diff$ 중 작은 값과 x에 num, y에 $y + 1$를 넣고 재귀 수행한 결과와 result 중 작은 값을 넣어준다.
- dp[x][y]에 $result + 1$를 넣어주고 해당 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FreedomTrail.java){:target="_blank"}에서 확인 가능합니다.