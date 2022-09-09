---
title: "Leetcode Java Two Sum IV - Input is a BST"
excerpt: "Leetcode Two Sum IV - Input is a BST"
last_modified_at: 2022-09-09T10:30:00
header:
  image: /assets/images/leetcode/two-sum-iv-input-is-a-bst.png
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
[Link](https://leetcode.com/problems/two-sum-iv-input-is-a-bst){:target="_blank"}

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

  public boolean findTarget(TreeNode root, int k) {
    return this.dfs(root, root, k);
  }

  private boolean dfs(TreeNode root, TreeNode curr, int k) {
    if (curr == null) {
      return false;
    } else {
      return this.search(root, curr, k - curr.val)
          || this.dfs(root, curr.left, k)
          || this.dfs(root, curr.right, k);
    }
  }

  private boolean search(TreeNode root, TreeNode curr, int k) {
    if (root == null) {
      return false;
    } else {
      return ((root.val == k) && (root != curr))
          || ((root.val < k) && this.search(root.right, curr, k))
          || ((root.val > k) && this.search(root.left, curr, k));
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/795158029/){:target="_blank"}

# 설명
1. root의 자식 노드들 중 두 TreeNode의 값을 이용해서 k를 만들 수 있는지 검증하는 문제이다.

2. 3번에서 정의한 dfs(TreeNode root, TreeNode curr, int k) 메서드에 root를 root와 curr 자리에 넣어 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 탐색할 dfs(TreeNode root, TreeNode curr, int k) 메서드를 정의한다.
- curr이 null인 경우 수행이 불가능하므로, false를 반환한다.
- 그렇지 않은 경우 아래의 경우 중 하나라도 만족하면 true를, 아니면 false를 반환한다.
  - 4번에서 정의한 search(TreeNode root, TreeNode curr, int k) 메서드에 $k - curr.val$를 k 자리에 넣어 수행 결과가 true인 경우.
  - curr의 left TreeNode를 이용하여 재귀 호출한 결과가 true인 경우.
  - curr의 right TreeNode를 이용하여 재귀 호출한 결과가 true인 경우.

4. root 기준으로 탐색하기 위한 search(TreeNode root, TreeNode curr, int k) 메서드를 정의한다.
- root가 null인 경우 수행이 불가능하므로, false를 반환한다.
- 그렇지 않은 경우 아래의 결과 중 하나라도 만족하면 true를, 아니면 false를 반환한다.
  - root의 val 값이 k와 동일하고 root와 curr이 다른 경우.
  - root의 val 값이 k보다 작고, root의 right TreeNode를 이용하여 재귀 호출한 결과가 true인 경우.
  - root의 val 값이 k보다 크고, root의 left TreeNode를 이용하여 재귀 호출한 결과가 true인 경우.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TwoSumIVInputIsABST.java){:target="_blank"}에서 확인 가능합니다.