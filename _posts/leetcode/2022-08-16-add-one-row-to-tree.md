---
title: "Leetcode Java Add One Row to Tree"
excerpt: "Leetcode Add One Row to Tree Java"
last_modified_at: 2022-08-16T19:00:00
header:
  image: /assets/images/leetcode/add-one-row-to-tree.png
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
[Link](https://leetcode.com/problems/add-one-row-to-tree/){:target="_blank"}

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

  public TreeNode addOneRow(TreeNode root, int val, int depth) {
    if (root != null) {
      if (depth == 1) {
        TreeNode treeNode = new TreeNode(val);
        treeNode.left = root;
        return treeNode;
      } else if (depth == 2) {
        TreeNode left = new TreeNode(val);
        left.left = root.left;
        TreeNode right = new TreeNode(val);
        right.right = root.right;
        root.left = left;
        root.right = right;
      } else {
        root.left = this.addOneRow(root.left, val, depth - 1);
        root.right = this.addOneRow(root.right, val, depth - 1);
      }
    }
    return root;
  }
  
}
```

# 결과
[Link](https://leetcode.com/submissions/detail/775049230/){:target="_blank"}

# 설명
1. root의 depth번째 깊이에 val 값의 TreeNode를 아래대로 수행한 결과를 반환하는 문제이다.
- depth가 주어지면 null이 아닌 cur TreeNode를 두 개 만들어 cur의 left TreeNode와 right TreeNode에 이어준다.
- cur의 기존 left TreeNode는 새 TreeNode의 left TreeNode로 넣어준다.
- cur의 기존 right TreeNode는 새 TreeNode의 right TreeNode로 넣어준다. 
- depth가 1인 경우, val 값인 TreeNode를 만들어 root를 앞에서 만든 TreeNode의 left TreeNode로 넣어준다.

2. root가 null이면 그대로 root를 반환한다.

3. depth가 1인 경우 val 값인 TreeNode를 treeNode로 정의하고, treeNode의 left TreeNode에 root를 넣어 treeNode를 반환한다.

4. depth가 1인 경우 아래를 수행한다.
- val 값인 TreeNode를 left와 right 두 개를 만든다.
- left의 left TreeNode에 root의 TreeNode를, right의 right TreeNode에 root의 right TreeNode를 넣어준다.
- root의 left TreeNode에 left를, root의 right TreeNode에 right를 넣어준다.

5. 그 외의 경우 아래를 수행한다.
- root의 left TreeNode에 root의 left TreeNode와 depth를 1 감소시킨 값으로 재귀 호출 수행한 결과를 넣어준다.
- root의 right TreeNode에 root의 right TreeNode와 depth를 1 감소시킨 값으로 재귀 호출 수행한 결과를 넣어준다.

6. 수행이 완료되면 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AddOneRowToTree.java){:target="_blank"}에서 확인 가능합니다.