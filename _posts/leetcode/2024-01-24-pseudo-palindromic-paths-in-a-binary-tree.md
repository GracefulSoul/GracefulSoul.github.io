---
title: "Leetcode Java Pseudo-Palindromic Paths in a Binary Tree"
excerpt: "Leetcode Medium - 'Pseudo-Palindromic Paths in a Binary Tree' 문제 Java 풀이"
last_modified_at: 2024-01-24T20:20:00
header:
  image: /assets/images/leetcode/pseudo-palindromic-paths-in-a-binary-tree.png
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
[Link](https://leetcode.com/problems/pseudo-palindromic-paths-in-a-binary-tree){:target="_blank"}

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

  public int pseudoPalindromicPaths(TreeNode root) {
    return this.dfs(root, 0);
  }

  private int dfs(TreeNode root, int count) {
    if (root == null) {
      return 0;
    }
    count ^= 1 << (root.val - 1);
    int result = this.dfs(root.left, count) + this.dfs(root.right, count);
    if (root.left == root.right && (count & (count - 1)) == 0) {
      result++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/pseudo-palindromic-paths-in-a-binary-tree/submissions/1155474239/){:target="_blank"}

# 설명
1. root의 루트 노드부터 리프 노드까지 값들을 이어준 값 중 최소 한 개 이상의 값을 재 배열하였을 때, 앞과 뒤가 동일한 문자열(이하 회문)이 되는 경우의 수를 구하는 문제이다.

2. 3번에서 정의한 dfs(TreeNode root, int count) 메서드를 count에 0을 넣고 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 회문이 되는 문자열을 검증하기 위한 dfs(TreeNode root, int count) 메서드를 정의한다.
- root가 null인 경우, 이어줄 값이 없으므로 0을 반환한다.
- count에 count와 1의 비트를 $root.val - 1$번 좌측으로 이동한 값의 XOR(^) 비트 연산을 수행한 결과를 넣어준다.
- result는 경우의 수를 계산하기 위한 변수로, root의 left와 right TreeNode를 순차적으로 count를 활용하여 재귀 호출한 결과를 더해서 넣어준다.
- root의 left와 right TreeNode가 null이면서 count와 $count - 1$을 AND(&) 비트 연산을 수행한 결과가 0인 경우, 회문을 만들 수 있으므로 result를 증가시킨다.
- 계산된 회문이 가능한 경우인 result를 반환한다.

# 해설
- TreeNode의 값은 [1, 9] 범위 내 값으로 이루어져 있으며, 회문이 되는 경우 XOR(^) 비트 연산을 수행하면 단 하나의 값만 남게 된다.
- 위의 조건을 기반으로 1을 좌측으로 8번 이동시켜도 $2^8 = 256$이 되므로, count에 자신의 값과 1을 $root.val - 1$번 좌측으로 이동시킨 값을 XOR(^) 연산을 root 노드부터 leaf 노드까지 모두 수행하였을 때 회문이 되는 경우는 단 하나의 1 비트만 존재하는 경우이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PseudoPalindromicPathsInABinaryTree.java){:target="_blank"}에서 확인 가능합니다.