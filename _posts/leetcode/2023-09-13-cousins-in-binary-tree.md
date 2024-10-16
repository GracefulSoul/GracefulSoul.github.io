---
title: "Leetcode Java Cousins in Binary Tree"
excerpt: "Leetcode Cousins in Binary Tree Java"
last_modified_at: 2023-09-13T18:30:00
header:
  image: /assets/images/leetcode/cousins-in-binary-tree.png
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
[Link](https://leetcode.com/problems/cousins-in-binary-tree){:target="_blank"}

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

  public boolean isCousins(TreeNode root, int x, int y) {
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()) {
      int size = queue.size();
      boolean foundX = false;
      boolean foundY = false;
      for (int i = 0; i < size; i++) {
        TreeNode curr = queue.poll();
        if (curr.val == x) {
          foundX = true;
        }
        if (curr.val == y) {
          foundY = true;
        }
        if (curr.left != null && curr.right != null) {
          if ((curr.left.val == x && curr.right.val == y) || (curr.left.val == y && curr.right.val == x)) {
            return false;
          }
        }
        if (curr.left != null) {
          queue.offer(curr.left);
        }
        if (curr.right != null) {
          queue.offer(curr.right);
        }
      }
      if (foundX && foundY) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/cousins-in-binary-tree/submissions/1048241981/){:target="_blank"}

# 설명
1. root에서 x와 y가 사촌 노드의 값인지 검증하는 문제이다.
- 사촌 노드는 서로 동일한 깊이의 다른 부모 노드를 가진 노드들을 의미한다.

2. queue는 동일한 깊이의 노드들을 탐색하기 위한 변수로, LinkedList로 초기화하고 root를 초기값으로 넣어준다.

3. queue가 비어있지 않을 때 까지 아래를 반복한다.
- size에 queue의 크기를 넣어준다.
- foundX와 foundY는 x와 y를 찾을 변수로, 둘 다 false로 초기화한다.
- 0부터 size 미만까지 i를 증가시키면서 아래를 반복한다.
  - curr에 queue에서 꺼낸 TreeNode를 넣어준다.
  - curr의 값이 x와 같으면 foundX를 true로, y와 같으면 foundY를 true로 바꾸어준다.
  - curr의 자식 노드가 모두 존재하는 경우, 자식 노드들의 값이 x와 y인 경우 사촌 노드가 아니므로 false를 주어진 문제의 결과로 반환한다.
  - curr의 자식 노드들이 존재하면 queue에 좌측부터 순차적으로 넣어준다.
- foundX와 foundY가 true인 사촌 노드이면, true를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 사촌 노드가 아니므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CousinsInBinaryTree.java){:target="_blank"}에서 확인 가능합니다.