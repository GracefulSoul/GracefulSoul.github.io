---
title: "Leetcode Java Longest Univalue Path"
excerpt: "Leetcode Longest Univalue Path Java"
last_modified_at: 2022-10-08T10:25:00
header:
  image: /assets/images/leetcode/longest-univalue-path.png
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
[Link](https://leetcode.com/problems/longest-univalue-path){:target="_blank"}

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

  private int length;

  public int longestUnivaluePath(TreeNode root) {
    if (root == null) {
      return 0;
    } else {
      this.length = 0;
      this.getLength(root, root.val);
      return this.length;
    }
  }

  private int getLength(TreeNode node, int val) {
    if (node == null) {
      return 0;
    }
    int left = this.getLength(node.left, node.val);
    int right = this.getLength(node.right, node.val);
    this.length = Math.max(this.length, left + right);
    if (val == node.val) {
      return Math.max(left, right) + 1;
    } else {
      return 0;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/817547458/){:target="_blank"}

# 설명
1. root 내 동일한 값을 가지는 노드들의 연결 선의 수가 가장 긴 값을 찾는 문제이다.

2. length는 root 내 동일한 값을 가지는 노드들의 연결 선의 수가 가장 긴 값을 저장할 변수이다.

3. root가 null인 경우 계산이 불가능하므로, 0을 주어진 문제의 결과로 반환한다.

4. root가 null이 아니면, length를 0으로 초기화하고 5번에서 정의한 getLength(TreeNode node, int val)를 이용하여 length에 가장 긴 연결 선의 수를 계산해 넣어준 후 length를 주어진 문제의 결과로 반환한다.

5. root를 이용하여 length에 가장 긴 연결 선의 수를 넣어줄 getLength(TreeNode node, int val) 메서드를 정의한다.
- node가 null인 경우, 연결 선의 수가 없으므로 0을 반환한다.
- left에 node의 left TreeNode와 node의 val 값을 이용해서 재귀 호출한 결과를 넣어준다.
- right에 node의 right TreeNode와 node의 val 값을 이용해서 재귀 호출한 결과를 넣어준다.
- length에 length와 $left + right$ 중 큰 값인 긴 연결 선의 수를 넣어준다.
- val이 node의 val 값과 동일한 경우, left와 right 중 큰 값에 호출된 위치의 노드를 포함한 1을 더해 반환한다.
- val이 node의 val 값과 동일하지 않은 경우 동일한 값을 가지는 연결된 노드가 아니므로, 0을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestUnivaluePath.java){:target="_blank"}에서 확인 가능합니다.