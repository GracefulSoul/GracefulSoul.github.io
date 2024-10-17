---
title: "Leetcode Java Minimum Depth of Binary Tree"
excerpt: "Leetcode - 'Minimum Depth of Binary Tree' 문제 Java 풀이"
last_modified_at: 2021-08-01T11:30:00
header:
  image: /assets/images/leetcode/minimum-depth-of-binary-tree.png
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
[Link](https://leetcode.com/problems/minimum-depth-of-binary-tree/){:target="_blank"}

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

  public int minDepth(TreeNode root) {
    if (root == null) {
      return 0;
    }
    List<TreeNode> queue = new ArrayList<>();
    queue.add(root);
    int depth = 1;
    while (!queue.isEmpty()) {
      int queueSize = queue.size();
      for (int idx = 0; idx < queueSize; idx++) {
        TreeNode treeNode = queue.remove(0);
        if (treeNode.left == null && treeNode.right == null) {
          return depth;
        }
        if (treeNode.left != null) {
          queue.add(treeNode.left);
        }
        if (treeNode.right != null) {
          queue.add(treeNode.right);
        }
      }
      depth++;
    }
    return depth;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/531329595/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root의 최소 깊이를 구하는 문제이다.

2. root가 null인 경우 최소 깊이를 구할 수 없으므로, 0을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- TreeNode의 각 노드 값을 임시 저장하기 위한 Queue 역할을 수행할 List를 정의하고, root를 초기 값으로 넣어준다.
- 최소 깊이를 계산할 변수 depth를 1로 정의한다.

4. queue가 비어있지 않을 때까지 반복하여 아래를 수행한다.
- queue에 저장된 개수를 먼저 임시 저장하고 해당 횟수만큼 반복하여 TreeNode를 검증한다.
- queue에 저장된 첫 TreeNode를 꺼내온다.
- 해당 treeNode의 left와 right가 null인 경우 자식이 없는 끝단 노드이므로, depth를 주어진 문제의 결과로 반환한다.
- treeNode의 left가 null이 아닌 경우, queue에 해당 TreeNode를 넣어준다.
- treeNode의 right가 null이 아닌 경우, queue에 해당 TreeNode를 넣어준다.
- queue에 저장된 횟수만큼 반복이 끝나면 depth를 증가시키고 맨 처음의 반복을 수행해준다.

5. 반복이 완료되면 최소 깊이를 저장한 변수 depth를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumDepthOfBinaryTree.java){:target="_blank"}에서 확인 가능합니다.