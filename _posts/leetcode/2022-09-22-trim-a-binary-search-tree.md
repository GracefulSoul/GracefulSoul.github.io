---
title: "Leetcode Java Trim a Binary Search Tree"
excerpt: "Leetcode Trim a Binary Search Tree Java"
last_modified_at: 2022-09-22T19:00:00
header:
  image: /assets/images/leetcode/trim-a-binary-search-tree.png
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
[Link](https://leetcode.com/problems/trim-a-binary-search-tree){:target="_blank"}

# 코드
```java
class Solution {

  public TreeNode trimBST(TreeNode root, int low, int high) {
    if (root == null) {
      return null;
    } else if (root.val < low) {
      return this.trimBST(root.right, low, high);
    } else if (root.val > high) {
      return this.trimBST(root.left, low, high);
    } else {
      root.left = this.trimBST(root.left, low, high);
      root.right = this.trimBST(root.right, low, high);
      return root;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/805989501/){:target="_blank"}

# 설명
1. root의 val 값들을 [low, high] 범위에 위치하도록 root를 수정하는 문제이다.

2. root가 null인 경우 수정할 항목이 없으므로, null을 반환한다.

3. 위의 경우가 아니면서 root의 val 값이 low보다 작은 경우 해당 TreeNode를 무시하고 root의 right TreeNode를 이용하여 재귀 호출한 결과를 반환한다.

4. 위의 경우가 아니면서 root의 val 값이 high보다 큰 경우 해당 TreeNode를 무시하고 root의 left TreeNode를 이용하여 재귀 호출한 결과를 반환한다.

5. 위의 모든 경우가 아닌 경우 정상적인 노드이므로 아래를 수행하고 root를 반환한다.
- root의 left TreeNode에 해당 TreeNode로 재귀 호출한 결과를 이어준다.
- root의 right TreeNode에 해당 TreeNode로 재귀 호출한 결과를 이어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TrimABinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.