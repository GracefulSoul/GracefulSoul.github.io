---
title: "Leetcode Java Sum Root to Leaf Numbers"
excerpt: "Leetcode - 'Sum Root to Leaf Numbers' 문제 Java 풀이"
last_modified_at: 2021-08-18T12:00:00
header:
  image: /assets/images/leetcode/sum-root-to-leaf-numbers.png
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
[Link](https://leetcode.com/problems/sum-root-to-leaf-numbers/){:target="_blank"}

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

  public int sumNumbers(TreeNode root) {
    return this.recursive(root, 0);
  }

  private int recursive(TreeNode node, int sum) {
    if (node == null) {
      return 0;
    } else if (node.left == null && node.right == null) {
      return sum * 10 + node.val;
    } else {
      return this.recursive(node.left, sum * 10 + node.val) + this.recursive(node.right, sum * 10 + node.val);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/540187160/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root를 이용하여 마지막 node까지 이동하며 val 값을 순차적으로 이어준 결과들을 합친 값을 구하는 문제이다.
- 아래의 예제를 보면, 1 -> 2, 1 -> 3으로 되어, 12 + 13인 25가 문제의 결과가 된다.
```text
 1
2 3
```

2. 재귀 호출을 이용하여 root 노드에서 부터 최종 합을 구하여 문제의 결과로 반환한다.
- node가 null인 경우, 마지막 노드이므로 해당 val 값은 0으로 반환한다.
- node의 left와 right가 null인 경우, 기존 더해진 sum에 10을 곱하고, node의 val 값을 더하여 반환한다.
- 그 외의 경우 node의 left와 right를 재귀 호출한 값의 합을 반환한다.
- 최종 재귀 호출을 수행하여 순차적으로 이어준 값의 합을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumRootToLeafNumbers.java){:target="_blank"}에서 확인 가능합니다.