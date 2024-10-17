---
title: "Leetcode Java Flip Equivalent Binary Trees"
excerpt: "Leetcode Medium - 'Flip Equivalent Binary Trees' 문제 Java 풀이"
last_modified_at: 2023-07-19T19:50:00
header:
  image: /assets/images/leetcode/flip-equivalent-binary-trees.png
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
[Link](https://leetcode.com/problems/flip-equivalent-binary-trees){:target="_blank"}

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

  public boolean flipEquiv(TreeNode root1, TreeNode root2) {
    if (root1 == null && root2 == null) {
      return true;
    } else if (root1 == null || root2 == null || root1.val != root2.val) {
      return false;
    } else if ((root1.left != null ? root1.left.val : -1) != (root2.left != null ? root2.left.val : -1)) {
      TreeNode temp = root1.left;
      root1.left = root1.right;
      root1.right = temp;
    }
    return this.flipEquiv(root1.left, root2.left) && this.flipEquiv(root1.right, root2.right);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/flip-equivalent-binary-trees/submissions/){:target="_blank"}

# 설명
1. root1의 각 노드의 위치에서 두 자식 노드 위치를 바꿔서 root2를 만들 수 있는지 검증하는 문제이다.

2. root1과 root2가 null인 경우, 동일하게 없는 노드의 위치이므로 true를 반환한다.

3. 2번의 경우가 아니면서 root1 혹은 root2가 null이거나 root1과 root2의 val값이 다른 경우, 노드가 다르므로 false를 반환한다.

4. 2, 3번의 경우가 아니면서 root1의 left과 right가 존재하는 경우 해당 값이 동일한 경우, root1의 left 노드와 right 노드의 위치를 변경한다.

5. 모든 경우가 수행되면 root1과 root2의 left 노드로 재귀 호출한 결과와 right 노드로 재귀 호출한 결과의 AND 조건의 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FlipEquivalentBinaryTrees.java){:target="_blank"}에서 확인 가능합니다.