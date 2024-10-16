---
title: "Leetcode Java Binary Tree Cameras"
excerpt: "Leetcode Binary Tree Cameras Java"
last_modified_at: 2023-08-05T19:20:00
header:
  image: /assets/images/leetcode/binary-tree-cameras.png
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
[Link](https://leetcode.com/problems/binary-tree-cameras){:target="_blank"}

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

  private int result;

  public int minCameraCover(TreeNode root) {
    this.result = 0;
    return (this.dfs(root) < 1 ? 1 : 0) + this.result;
  }

  public int dfs(TreeNode root) {
    if (root == null) {
      return 2;
    }
    int left = this.dfs(root.left);
    int right = this.dfs(root.right);
    if (left == 0 || right == 0) {
      this.result++;
      return 1;
    } else {
      return left == 1 || right == 1 ? 2 : 0;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/binary-tree-cameras/submissions/1012538417/){:target="_blank"}

# 설명
1. 이진 트리인 root를 전체 확인하기 위한 카메라의 최소 갯수를 구하는 문제이다.
- 카메라는 자신으로부터 부모와 자식 노드를 탐색할 수 있다.

2. result는 최소 카메라의 수를 저장하기 위한 변수이다.

3. result를 0으로 초기화하고, 4번에서 정의한 dfs(TreeNode root) 메서드를 수행한 결과가 1보다 작으면 1, 아니면 0에 result를 더해서 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 카메라의 최소 갯수를 탐색하기 위한 dfs(TreeNode root) 메서드를 정의한다.
- root가 null인 경우, 2를 반환한다.
- left에 root의 left TreeNode를 이용하여 재귀 호출을 수행한 값을 넣어준다.
- right에 root의 right TreeNode를 이용하여 재귀 호출을 수행한 값을 넣어준다.
- left가 0이거나 right가 0인 경우, result를 증가시키고 1을 반환한다.
- 위의 경우가 아니라면 left가 1이거나 right가 1인 경우, 2를 아니면 0을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreeCameras.java){:target="_blank"}에서 확인 가능합니다.