---
title: "Leetcode Java Reverse Odd Levels of Binary Tree"
excerpt: "Leetcode - 'Reverse Odd Levels of Binary Tree' 문제 Java 풀이"
last_modified_at: 2024-12-20T19:20:00
header:
  image: /assets/images/leetcode/reverse-odd-levels-of-binary-tree.png
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
[Link](https://leetcode.com/problems/reverse-odd-levels-of-binary-tree/){:target="_blank"}

# 코드
```java
class Solution {

  public TreeNode reverseOddLevels(TreeNode root) {
    this.dfs(root.left, root.right, 1);
    return root;
  }

  private void dfs(TreeNode node1, TreeNode node2, int level) {
    if (node1 != null && node2 != null) {
      if (level % 2 == 1) {
        int temp = node1.val;
        node1.val = node2.val;
        node2.val = temp;
      }
      this.dfs(node1.left, node2.right, level + 1);
      this.dfs(node1.right, node2.left, level + 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reverse-odd-levels-of-binary-tree/submissions/1483655049/){:target="_blank"}

# 설명
1. 이진 트리 노드인 root의 짝수번째 레벨에 해당하는 자식 노드들의 값을 바꾸는 문제이다.

2. 3번에서 정의한 dfs(TreeNode node1, TreeNode node2, int level)를 root의 left와 right 노드와 1을 순서대로 넣어 수행 후, 완성된 root를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 이진 트리 노드를 재 구성할 dfs(TreeNode node1, TreeNode node2, int level) 메서드를 정의한다.
- node1과 node2가 null이 아닌 경우만 아래를 수행한다.
  - level이 홀수이면 현재 node1과 node2는 짝수 레벨이므로, 두 노드의 val 값을 바꿔준다.
  - node1의 left 노드와 node2의 right 노드, level을 1 증가시킨 후 재귀 호출을 수행한다.
  - node1의 right 노드와 node2의 left 노드, level을 1 증가시킨 후 재귀 호출을 수행한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseOddLevelsOfBinaryTree.java){:target="_blank"}에서 확인 가능합니다.