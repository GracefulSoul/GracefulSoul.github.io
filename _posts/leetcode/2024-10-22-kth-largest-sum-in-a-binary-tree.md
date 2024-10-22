---
title: "Leetcode Java Kth Largest Sum in a Binary Tree"
excerpt: "Leetcode - 'Kth Largest Sum in a Binary Tree' 문제 Java 풀이"
last_modified_at: 2024-10-21T17:30:00
header:
  image: /assets/images/leetcode/kth-largest-sum-in-a-binary-tree.png
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
[Link](https://leetcode.com/problems/kth-largest-sum-in-a-binary-tree/){:target="_blank"}

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

  public long kthLargestLevelSum(TreeNode root, int k) {
    Queue<Long> result = new PriorityQueue<>();
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    while (!queue.isEmpty()) {
      int size = queue.size();
      long sum = 0;
      while (size-- > 0) {
        TreeNode temp = queue.poll();
        sum += temp.val;
        if (temp.left != null) {
          queue.add(temp.left);
        }
        if (temp.right != null) {
          queue.add(temp.right);
        }
      }
      result.add(sum);
      if (result.size() > k) {
        result.poll();
      }
    }
    return result.size() < k ? -1 : result.peek();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/kth-largest-sum-in-a-binary-tree/submissions/1430216236/){:target="_blank"}

# 설명
1. 이진 트리인 root의 레벨 별 값들의 합계를 구할 때, k번째 큰 합계를 반환하는 문제이다.
- 단, 트리의 레벨이 k 이하인 k번째 큰 합계가 존재하지 않으면 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 레벨 별 합계를 오름차순으로 관리하기 위한 변수로, PriorityQueue로 초기화한다.
- queue는 각 노드를 순차적으로 넣어 합계를 계산하기 위한 변수로, LinkedList로 초기화하고 root를 넣어준다.

3. queue가 비어있지 않을 때 까지 아래를 반복한다.
- size에 queue의 크기를 저장한 변수이고, 합계를 저장할 sum은 0으로 초기화한다.
- size가 0 초과일 때 까지 size를 감소시키며 아래를 반복한다.
  - temp에 queue의 노드를 꺼내 넣어준다.
  - sum에 temp의 val 값을 더해 합계를 계산한다.
  - queue에 temp의 left와 right 노드가 존재하면 순차적으로 넣어준다.
- result에 현재 레벨의 합계인 sum을 넣어준다.
- result의 크기가 k 초과이면 result에서 첫 값인 가장 작은 k 범위를 초과한 값을 제거해준다.

4. 반복이 완료되면 result의 길이가 k보다 작으면 k번째 값이 없으므로 -1을, 그렇지 않은 경우 result의 첫 값인 k번째 큰 합계를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KthLargestSumInABinaryTree.java){:target="_blank"}에서 확인 가능합니다.