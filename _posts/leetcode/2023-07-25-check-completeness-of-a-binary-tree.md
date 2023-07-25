---
title: "Leetcode Java Check Completeness of a Binary Tree"
excerpt: "Leetcode Check Completeness of a Binary Tree Java"
last_modified_at: 2023-07-25T19:40:00
header:
  image: /assets/images/leetcode/check-completeness-of-a-binary-tree.png
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
[Link](https://leetcode.com/problems/check-completeness-of-a-binary-tree){:target="_blank"}

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

  public boolean isCompleteTree(TreeNode root) {
    boolean lastNode = false;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    while (!queue.isEmpty()) {
      TreeNode curr = queue.poll();
      if (curr == null) {
        lastNode = true;
      } else if (lastNode) {
        return false;
      } else {
        queue.add(curr.left);
        queue.add(curr.right);
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-completeness-of-a-binary-tree/submissions/1003461143/){:target="_blank"}

# 설명
1. root가 완벽한 이진 트리인지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- lastNode는 이진 트리의 마지막 노드인지 검증하기 위한 변수로, false로 초기화한다.
- queue는 TreeNode를 순차적으로 넣고 검증하기 위한 변수로, LinkedList로 초기화하고 root를 넣어준다.

3. queue가 비어있지 않을 때 까지 아래를 반복한다.
- curr에 queue의 첫 TreeNode를 꺼내 넣어준다.
- curr이 null인 경우 TreeNode의 마지막 노드이므로, lastNode를 true로 바꾸어준다.
- 위의 경우가 아니라 lastNode가 true인 경우, 노드간 빈 노드가 존재하여 완벽한 이진 트리가 아니므로 false를 주어진 문제의 결과로 반환한다.
- 위의 모든 경우가 아니라면 curr의 left와 right TreeNode를 순차적으로 queue에 넣어준다.

4. 반복이 완료되면 root는 완벽한 이진 트리이므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckCompletenessOfABinaryTree.java){:target="_blank"}에서 확인 가능합니다.