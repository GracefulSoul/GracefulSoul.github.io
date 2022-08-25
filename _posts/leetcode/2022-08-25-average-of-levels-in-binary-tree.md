---
title: "Leetcode Java Average of Levels in Binary Tree"
excerpt: "Leetcode Average of Levels in Binary Tree Java"
last_modified_at: 2022-08-25T19:20:00
header:
  image: /assets/images/leetcode/average-of-levels-in-binary-tree.png
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
[Link](https://leetcode.com/problems/average-of-levels-in-binary-tree/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Double> averageOfLevels(TreeNode root) {
    List<Double> result = new ArrayList<>();
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    while (!queue.isEmpty()) {
      int size = queue.size();
      int count = size;
      double sum = 0;
      while (size-- > 0) {
        TreeNode treeNode = queue.poll();
        sum += treeNode.val;
        if (treeNode.left != null) {
          queue.add(treeNode.left);
        }
        if (treeNode.right != null) {
          queue.add(treeNode.right);
        }
      }
      result.add(sum / count);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/782965294/){:target="_blank"}

# 설명
1. root의 각 레벨 별 TreeNode의 평균 val 값을 List로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 각 레벨 별 TreeNode의 평균 val 값을 넣을 변수로, ArrayList로 초기화한다.
- queue는 각 레벨 별 TreeNode를 임시 저장할 변수로, LinkedList로 초기화하고 root를 넣어준다.

3. queue가 비어있지 않을 때까지 아래를 반복하여 수행한다.
- size에 queue의 크기를 저장한다.
- count는 sum을 나눌 TreeNode의 갯수인 size를 저장한다.
- 각 TreeNode의 합계를 저장할 sum은 실수로 구하기 위해 double로 정의하고, 0으로 초기화한다.
- size가 0 초과인 경우까지 아래를 다시 반복하고, size를 감소시킨다.
  - queue에 있는 값을 꺼내 treeNode에 임시 저장한다.
  - sum에 treeNode의 val 값을 저장하고, left와 right TreeNode가 존재하면 순차적으로 queue에 다시 넣어준다.
- 위의 반복이 완료되면 $\frac{sum}{count}$의 결과를 result에 넣고, 다시 처음부터 수행한다.

4. 반복이 완료되면 root의 각 레벨 별 TreeNode의 평균 val 값을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AverageOfLevelsInBinaryTree.java){:target="_blank"}에서 확인 가능합니다.