---
title: "Leetcode Java Sum of Root To Leaf Binary Numbers"
excerpt: "Leetcode Easy - 'Sum of Root To Leaf Binary Numbers' 문제 Java 풀이"
last_modified_at: 2024-01-16T18:20:00
header:
  image: /assets/images/leetcode/sum-of-root-to-leaf-binary-numbers.png
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
[Link](https://leetcode.com/problems/sum-of-root-to-leaf-binary-numbers){:target="_blank"}

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

  public int sumRootToLeaf(TreeNode root) {
    return this.dfs(root, 0);
  }

  private int dfs(TreeNode root, int val) {
    if (root == null) {
      return 0;
    } else {
      val = (val * 2) + root.val;
      return root.left == root.right ? val : this.dfs(root.left, val) + this.dfs(root.right, val);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sum-of-root-to-leaf-binary-numbers/submissions/1147678631/){:target="_blank"}

# 설명
1. 0과 1의 값들만 가진 root를 이용하여 root에서 leaf로 갈 때 순서대로의 이진 표현법이 최대가 되는 값을 구하는 문제이다.

2. 3번에서 정의한 dfs(TreeNode root, int val) 메서드의 val에 0을 넣고 수행한 결과를 주어진 문제의 결과로 반환한다.

3. root가 null인 노드가 없을 경우, 0을 반환한다.

4. root가 null이 아닌 경우, 아래를 수행한다.
- val에 $(val \times 2) + root.val$ 값을 넣어 이진 수를 계산한다.
- root의 left TreeNode와 right TreeNode가 동일 한 값인 null이면 더 이상 진행이 안되므로 val을, 아니면 left TreeNode와 right TreeNode를 각각 val을 이용하여 재귀 호출한 결과를 더해서 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfRootToLeafBinaryNumbers.java){:target="_blank"}에서 확인 가능합니다.