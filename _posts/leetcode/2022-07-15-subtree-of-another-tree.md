---
title: "Leetcode Java Subtree of Another Tree"
excerpt: "Leetcode - 'Subtree of Another Tree' 문제 Java 풀이"
last_modified_at: 2022-07-15T20:00:00
header:
  image: /assets/images/leetcode/subtree-of-another-tree.png
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
[Link](https://leetcode.com/problems/subtree-of-another-tree/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isSubtree(TreeNode root, TreeNode subRoot) {
    if ((root == null && subRoot != null) || (root != null && subRoot == null)) {
      return false;
    } else if (this.isSameTree(root, subRoot)) {
      return true;
    } else {
      return this.isSubtree(root.left, subRoot) || this.isSubtree(root.right, subRoot);
    }
  }

  private boolean isSameTree(TreeNode root, TreeNode subRoot) {
    if (root == null || subRoot == null) {
      return root == null && subRoot == null;
    } else if (root.val == subRoot.val) {
      return this.isSameTree(root.left, subRoot.left) && this.isSameTree(root.right, subRoot.right);
    } else {
      return false;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/747717491/){:target="_blank"}

# 설명
1. subRoot가 root의 하위 트리인지 검증하는 문제이다.

2. root가 null이고 subRoot가 null이 아니거나, root가 null이 아니고 subRoot가 null이면 하위 트리가 될 수 없는 구성이므로 false를 주어진 문제의 결과로 반환한다.

3. root와 subRoot가 5번에서 정의한 isSameTree(TreeNode root, TreeNode subRoot) 메서드를 만족하는 경우, true를 반환한다.

4. root의 left와 right TreeNode를 이용한 재귀 호출을 수행한 결과가 하나라도 만족하면 true를, 아니면 false를 반환한다.

5. 두 TreeNode가 동일한지 검증하기 위한 isSameTree(TreeNode root, TreeNode subRoot) 메서드를 정의한다.
- root와 subRoot 둘 중 하나라도 null인 경우, 둘 다 null인지 여부를 반환한다.
- root의 val 값과 subRoot의 val 값이 동일하면 root와 subRoot의 left와 right TreeNode를 이용하여 재귀 호출한 결과를 반환한다.
- 그 외의 경우 동일하지 않으므로 false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SubtreeOfAnotherTree.java){:target="_blank"}에서 확인 가능합니다.