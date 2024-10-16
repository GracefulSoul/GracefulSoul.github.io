---
title: "Leetcode Java Maximum Level Sum of a Binary Tree"
excerpt: "Leetcode Maximum Level Sum of a Binary Tree Java"
last_modified_at: 2024-08-14T17:50:00
header:
  image: /assets/images/leetcode/maximum-level-sum-of-a-binary-tree.png
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
[Link](https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/){:target="_blank"}

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

  public int maxLevelSum(TreeNode root) {
    int result = 1;
    int max = Integer.MIN_VALUE;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    for (int i = 1; !queue.isEmpty(); i++) {
      int sum = 0;
      for (int size = queue.size(); size > 0; size--) {
        TreeNode node = queue.poll();
        sum += node.val;
        if (node.left != null) {
          queue.offer(node.left);
        }
        if (node.right != null) {
          queue.offer(node.right);
        }
      }
      if (max < sum) {
        max = sum;
        result = i;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree/submissions/1355210252/){:target="_blank"}

# 설명
1. root의 동일한 레벨 별 노드들 값의 합이 최대인 레벨을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 동일한 레벨 별 노드들 값의 합이 최대인 레벨을 저장할 변수로, root 노드의 레벨인 1로 초기화한다.
- max는 동일한 레벨 별 노드들 값의 합을 저장할 변수로, 정수의 가장 작은 값으로 초기화한다.
- queue는 레벨 별 노드들을 넣어 계산에 활용할 변수로, LinkedList로 초기화하고 root를 넣어준다.

3. 1부터 queue가 비어있지 않을 때 까지 i를 증가시키며 아래를 반복한다.
- sum은 현재 레벨의 합계를 저장할 변수로 0으로 초기화한다.
- size는 queue의 크기부터 size가 0 초과일 때 까지 감소시키며 아래를 반복한다.
  - node에 queue의 앞의 값을 꺼내 넣어준다.
  - sum에 node의 값을 넣어준다.
  - node left와 right 자식 노드가 존재하면 순차적으로 queue에 넣어준다.
- max가 sum보다 작은 현재 레벨의 합계가 가장 큰 경우, max에 sum을 result에 i를 넣어준다.

4. 반복이 완료되면 동일한 레벨 별 노드들 값의 합이 최대인 레벨이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumLevelSumOfABinaryTree.java){:target="_blank"}에서 확인 가능합니다.