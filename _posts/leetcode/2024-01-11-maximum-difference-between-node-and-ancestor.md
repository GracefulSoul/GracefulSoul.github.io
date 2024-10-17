---
title: "Leetcode Java Maximum Difference Between Node and Ancestor"
excerpt: "Leetcode Medium - 'Maximum Difference Between Node and Ancestor' 문제 Java 풀이"
last_modified_at: 2024-01-11T09:40:00
header:
  image: /assets/images/leetcode/maximum-difference-between-node-and-ancestor.png
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
[Link](https://leetcode.com/problems/maximum-difference-between-node-and-ancestor){:target="_blank"}

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

  public int maxAncestorDiff(TreeNode root) {
    return dfs(root, root.val, root.val);
  }

  private int dfs(TreeNode root, int max, int min) {
    if (root == null) {
      return max - min;
    } else {
      max = Math.max(max, root.val);
      min = Math.min(min, root.val);
      return Math.max(this.dfs(root.left, max, min), this.dfs(root.right, max, min));
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-difference-between-node-and-ancestor/submissions/1142865196/){:target="_blank"}

# 설명
1. root의 상위 노드와 하위 노드의 차이가 가장 큰 값을 찾는 문제이다.

2. 3번에서 정의한 dfs(TreeNode root, int max, int min) 메서드의 각 정수 값에 root.val 값을 넣어 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS방식으로 최대 차잇값을 구하기 위한 dfs(TreeNode root, int max, int min) 메서드를 정의한다.
- root가 null인 leaf노드인 경우, 현재까지의 최댓값과 최솟값의 차이인 $max - min$을 반환한다.
- root가 null이 아니면 아래를 수행한다.
  - max와 min에 root의 val값과 비교한 값을 다시 넣어준다.
  - root의 left와 right TreeNode로 재귀 호출한 결과 중 큰 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumDifferenceBetweenNodeAndAncestor.java){:target="_blank"}에서 확인 가능합니다.