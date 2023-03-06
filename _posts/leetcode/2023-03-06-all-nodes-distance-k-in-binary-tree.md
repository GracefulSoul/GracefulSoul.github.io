---
title: "Leetcode Java All Nodes Distance K in Binary Tree"
excerpt: "Leetcode All Nodes Distance K in Binary Tree Java"
last_modified_at: 2023-03-06T18:55:00
header:
  image: /assets/images/leetcode/all-nodes-distance-k-in-binary-tree.png
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
[Link](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree){:target="_blank"}

# 코드
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {

  public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
    List<Integer> result = new ArrayList<>();
    if (k == 0) {
      result.add(target.val);
    } else {
      this.dfs(root, target.val, k, 0, result);
    }
    return result;
  }

  private int dfs(TreeNode node, int target, int k, int depth, List<Integer> result) {
    if (node == null) {
      return 0;
    } else if (depth == k) {
      result.add(node.val);
      return 0;
    }
    int correction = node.val == target || depth > 0 ? 1 : 0;
    int left = this.dfs(node.left, target, k, depth + correction, result);
    int right = this.dfs(node.right, target, k, depth + correction, result);
    if (node.val == target) {
      return 1;
    } else if (left == k || right == k) {
      result.add(node.val);
      return 0;
    } else if (left > 0) {
      this.dfs(node.right, target, k, left + 1, result);
      return left + 1;
    } else if (right > 0) {
      this.dfs(node.left, target, k, right + 1, result);
      return right + 1;
    } else {
      return 0;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/submissions/910084313/){:target="_blank"}

# 설명
1. root에서 target과 거리가 k인 모든 노드의 값을 반환하는 문제이다.

2. result는 target과 거리가 k인 모든 노드의 값을 저장할 변수로, ArrayList로 초기화한다.

3. k가 0이면 자기 자신만 포함되므로, result에 target의 값을 넣어주고 아니면 4번에서 정의한 dfs(TreeNode node, int target, int k, int depth, List<Integer> result) 메서드를 depth에 0을 넣고 수행한다.

4. DFS 방식으로 target과의 거리를 탐색할 dfs(TreeNode node, int target, int k, int depth, List<Integer> result) 메서드를 정의한다.
- node가 null이면 0을, depth가 k와 동일하면 result에 node의 val 값을 넣어주고 0을 반환한다.
- correction에 node의 값과 target 이 동일하거나 depth가 0보다 크면 1을, 아니면 0을 넣어 거리를 초기화한다.
- left에 node의 left TreeNode를 넣고, depth에 correction을 더해서 재귀 호출한 값을 넣어준다.
- right에 node의 right TreeNode를 넣고, depth에 correction을 더해서 재귀 호출한 값을 넣어준다.
- 아래의 각 경우를 순차적으로 검증하여 거리에 대한 값을 반환한다.
  - node의 val 값이 target과 동일하면 1을 반환한다.
  - left 혹은 right가 k이면 result에 node의 값을 넣어주고 0을 반환하여 초기화한다.
  - left가 0보다 큰 경우, node의 right TreeNode와 depth에 $right + 1$을 넣어 재귀 호출한 이후 $left + 1$을 반환하여 거리를 증가시킨다.
  - right가 0보다 큰 경우, node의 left TreeNode와 depth에 $left + 1$을 넣어 재귀 호출한 이후 $right + 1$을 반환하여 거리를 증가시킨다.
  - 위의 모든 경우가 아니면 0을 반환하여 처음부터 계산을 수행한다.

5. 수행이 완료되면 모든 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AllNodesDistanceKInBinaryTree.java){:target="_blank"}에서 확인 가능합니다.