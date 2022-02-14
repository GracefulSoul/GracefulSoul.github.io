---
title: "Leetcode Java Lexicographical Numbers"
excerpt: "Leetcode Lexicographical Numbers Java 풀이"
last_modified_at: 2022-02-14T13:00:00
header:
  image: /assets/images/leetcode/lexicographical-numbers.png
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
[Link](https://leetcode.com/problems/lexicographical-numbers/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> lexicalOrder(int n) {
    List<Integer> result = new ArrayList<>();
    for (int idx = 1; idx < 10; idx++) {
      this.dfs(result, n, idx);
    }
    return result;
  }

  private void dfs(List<Integer> result, int n, int curr) {
    if (curr > n) {
      return;
    }
    result.add(curr);
    for (int idx = 0; idx < 10; idx++) {
      if ((10 * curr) + idx > n) {
        return;
      }
      this.dfs(result, n, (10 * curr) + idx);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/640983194/){:target="_blank"}

# 설명
1. 1부터 주어진 정수 n까지 사전 순으로 정렬하여 반환하는 문제이다.
- O(n) 시간 복잡도와, O(1) 공간 복잡도를 사용하는 알고리즘을 작성해야 한다.

2. 결과를 저장할 result를 ArrayList로 초기화하고 1부터 10 미만까지 idx를 증가시키며 반복하여, 3번에서 정의한 dfs(List<Integer> result, int n, int curr) 메서드를 수행한다.

3. [DFS 알고리즘](https://en.wikipedia.org/wiki/Depth-first_search){:target="_blank"}로 문자열 탐색을 수행하는 dfs(List<Integer> result, int n, int curr) 메서드를 완성한다.
- curr이 n보다 큰 경우 기준을 초과되었으므로, 그만 수행한다.
- result에 curr을 넣어준다.
- 0부터 10 미만까지 idx를 증가시키며 반복을 수행한다.
  - $(10 \times curr) + idx$이 n보다 큰 경우 기준을 초과하였으므로, 그만 수행한다.
  - 재귀 호출을 통해 curr에 $(10 \times curr) + idx$을 넣어 사전 순으로 정수를 result에 넣어준다.

4. 2번의 반복이 완료되면 결과를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LexicographicalNumbers.java){:target="_blank"}에서 확인 가능합니다.