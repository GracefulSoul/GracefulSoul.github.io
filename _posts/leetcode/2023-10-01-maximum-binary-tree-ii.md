---
title: "Leetcode Java Maximum Binary Tree II"
excerpt: "Leetcode Maximum Binary Tree II Java"
last_modified_at: 2023-10-01T12:45:00
header:
  image: /assets/images/leetcode/maximum-binary-tree-ii.png
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
[Link](https://leetcode.com/problems/maximum-binary-tree-ii){:target="_blank"}

# 코드
```java
class Solution {

  public TreeNode insertIntoMaxTree(TreeNode root, int val) {
    if (root == null || val > root.val) {
      TreeNode treeNode = new TreeNode(val);
      treeNode.left = root;
      return treeNode;
    } else {
      root.right = this.insertIntoMaxTree(root.right, val);
      return root;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-binary-tree-ii/submissions/1063657701/){:target="_blank"}

# 설명
1. 이진 트리 노드인 root에 val에 해당하는 노드를 이어주는 문제이다.
- 단, b는 a에 존재하지 않는 값이다.

2. root가 null이거나 val이 root의 val 값보다 큰 경우, 아래를 수행한다.
- treeNode에 val을 이용하여 새 TreeNode를 생성하여 treeNode의 left 자식 노드에 root를 넣은 후 treeNode를 반환한다.

3. 위의 경우가 아니라면 root의 right 자식 노드 자리에 root의 right TreeNode를 이용하여 재귀 호출한 결과를 넣어주고 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumBinaryTreeII.java){:target="_blank"}에서 확인 가능합니다.