---
title: "Leetcode Java Find Largest Value in Each Tree Row"
excerpt: "Leetcode Find Largest Value in Each Tree Row Java"
last_modified_at: 2022-05-31T12:00:00
header:
  image: /assets/images/leetcode/find-largest-value-in-each-tree-row.png
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

  public List<Integer> largestValues(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    this.dfs(root, result, 0);
    return result;
  }

  private void dfs(TreeNode root, List<Integer> result, int level) {
    if (root != null) {
      if (result.size() == level) {
        result.add(root.val);
      } else {
        if (root.val > result.get(level)) {
          result.set(level, root.val);
        }
      }
      this.dfs(root.left, result, level + 1);
      this.dfs(root.right, result, level + 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/710913581/){:target="_blank"}

# 설명
1. root의 level 별 가장 큰 값들을 반환하는 문제이다.

2. 결과를 저장할 result 배열을 ArrayList로 정의한다.

3. 4번에서 정의한 dfs(TreeNode root, List<Integer> result, int level) 메서드를 level에 0을 넣어 수행한다.

4. DFS 방식으로 각 층 별 큰 값을 result에 넣기 위한 dfs(TreeNode root, List<Integer> result, int level) 메서드를 정의한다.
- root가 null이 아닌 경우만 아래를 수행한다.
- result의 크기와 level이 동일한 경우 해당 level의 첫 수행이므로, root의 val 값을 우선 넣어준다.
- result의 크기와 level이 다른 경우 각 level의 값이 있으므로, result에서 level에 해당하는 위치의 값과 root의 val 값을 비교해서 큰 값을 result의 level에 해당하는 위치에 넣어준다.
- root의 left와 right TreeNode로 level을 1 증가시켜 각각 재귀 호출을 수행한다.

5. 수행이 완료되면 root의 각 level 별 가장 큰 값을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindLargestValueInEachTreeRow.java){:target="_blank"}에서 확인 가능합니다.