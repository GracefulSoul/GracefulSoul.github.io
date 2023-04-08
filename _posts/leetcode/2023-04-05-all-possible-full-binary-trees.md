---
title: "Leetcode Java All Possible Full Binary Trees"
excerpt: "Leetcode All Possible Full Binary Trees Java"
last_modified_at: 2023-04-05T19:20:00
header:
  image: /assets/images/leetcode/all-possible-full-binary-trees.png
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
[Link](https://leetcode.com/problems/all-possible-full-binary-trees){:target="_blank"}

# 코드
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

  public List<TreeNode> allPossibleFBT(int n) {
    return this.dfs(n, new HashMap<>());
  }

  private List<TreeNode> dfs(int n, Map<Integer, List<TreeNode>> map) {
    if (!map.containsKey(n)) {
      List<TreeNode> nodeList = new ArrayList<TreeNode>();
      if (n == 1) {
        TreeNode node = new TreeNode(0);
        nodeList.add(node);
      } else if (n % 2 == 1) {
        for (int x = 0; x < n; x++) {
          int y = n - 1 - x;
          for (TreeNode left : this.dfs(x, map)) {
            for (TreeNode right : this.dfs(y, map)) {
              TreeNode node = new TreeNode(0);
              node.left = left;
              node.right = right;
              nodeList.add(node);
            }
          }
        }
      }
      map.put(n, nodeList);
    }
    return map.get(n);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/all-possible-full-binary-trees/submissions/928391175/){:target="_blank"}

# 설명
1. 노드가 n개인 가능한 모든 이진 TreeNode를 반환하는 문제이다.
- 단, 각 노드의 값은 0이어야 한다.

2. 3번에서 정의한 dfs(int n, Map<Integer, List<TreeNode>> map) 메서드에 n과 새 HashMap을 넣어 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 TreeNode의 모든 조합을 만들 dfs(int n, Map<Integer, List<TreeNode>> map) 메서드를 완성한다.
- map에 n이 키인 값이 존재하는 경우, 아래를 수행한다.
  - n이 1인 경우, 조합의 결과를 넣을 nodeList에 root인 TreeNode를 정의하여 키가 1인 값으로 넣어준다.
  - n이 홀수인 경우 자녀 노드를 이어야 하므로, 0부터 n 미만까지 x를 증가시키며 아래를 계속 수행한다.
  - y에 $n - 1 - x$를 넣고, x와 map을 이용하여 모든 값에 left를 y와 map을 이용하여 모든 값에 right를 넣어 새 TreeNode의 left TreeNode와 right TreeNode에 차례대로 넣어 noeList에 넣어준다.
- map의 n번째 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AllPossibleFullBinaryTrees.java){:target="_blank"}에서 확인 가능합니다.