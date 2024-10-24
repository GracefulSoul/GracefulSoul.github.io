---
title: "Leetcode Java Cousins in Binary Tree II"
excerpt: "Leetcode - 'Cousins in Binary Tree II' 문제 Java 풀이"
last_modified_at: 2024-10-24T17:30:00
header:
  image: /assets/images/leetcode/cousins-in-binary-tree-ii.png
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
[Link](https://leetcode.com/problems/cousins-in-binary-tree-ii/){:target="_blank"}

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

  public TreeNode replaceValueInTree(TreeNode root) {
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    int curr = root.val;
    while (!queue.isEmpty()) {
      int next = 0;
      int size = queue.size();
      while (size-- > 0) {
        TreeNode node = queue.poll();
        TreeNode left = node.left;
        TreeNode right = node.right;
        node.val = curr - node.val;
        if (left != null) {
          queue.offer(left);
          next += left.val;
        }
        if (right != null) {
          queue.offer(right);
          next += right.val;
        }
        if (left != null && right != null) {
          int sum = left.val + right.val;
          left.val = right.val = sum;
        }
      }
      curr = next;
    }
    return root;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/cousins-in-binary-tree-ii/submissions/1431221928/){:target="_blank"}

# 설명
1. 이진 트리인 root에서 부모가 다른 동일한 레벨 내 노드들 값의 합을 각 노드에 넣어주는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- queue는 각 레벨 별 노드를 넣어 보관할 변수로, LinkedList로 초기화하여 root를 넣어준다.
- curr은 노드의 값을 설정하기 위한 변수로, root의 val 값으로 초기화한다.

3. queue가 비어있지 않을 때 까지 아래를 반복한다.
- 반복에 필요한 변수를 정의한다.
  - next는 curr에 넣을 값을 저장할 변수로, 0으로 초기화한다.
  - size는 현재 queue에 존재하는 값의 갯수를 저장할 변수이다.
- size가 0 초과일 때 까지 size를 감소시키며 아래를 반복한다.
  - node에 queue 맨 앞의 노드를 넣어주고, left와 right에 각 left와 right 노드를 넣어준다.
  - node의 val 값에 $curr - node.val$인 차감된 노드의 값을 넣어준다.
  - left가 null이 아닌 경우, queue에 left 노드를 넣고 next에 left 노드의 val 값을 더해준다.
  - right가 null이 아닌 경우, queue에 right 노드를 넣고 next에 right 노드의 val 값을 더해준다.
  - left 노드와 right 노드가 존재하는 경우, left 노드와 right 노드에 두 노드 val 값의 합을 넣어준다.
- 위의 반복이 완료되면 curr에 next를 넣어 다음 노드 계산에 자식 노드 합계로 계산하도록 한다.

4. 반복이 완료되면 root를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CousinsInBinaryTreeII.java){:target="_blank"}에서 확인 가능합니다.