---
title: "Leetcode Java Find Elements in a Contaminated Binary Tree"
excerpt: "Leetcode - 'Find Elements in a Contaminated Binary Tree' 문제 Java 풀이"
last_modified_at: 2025-02-21T11:40:00
header:
  image: /assets/images/leetcode/find-elements-in-a-contaminated-binary-tree.png
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
[Link](https://leetcode.com/problems/find-elements-in-a-contaminated-binary-tree/){:target="_blank"}

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
class FindElements {

  private BitSet bitSet;

  public FindElements(TreeNode root) {
    root.val = 0;
    this.bitSet = new BitSet();
    this.bfs(root);
  }

  public boolean find(int target) {
    return this.bitSet.get(target);
  }

  private void bfs(TreeNode node) {
    this.bitSet.set(node.val);
    if (node.left != null) {
      node.left.val = (2 * node.val) + 1;
      this.bfs(node.left);
    }
    if (node.right != null) {
      node.right.val = (2 * node.val) + 2;
      this.bfs(node.right);
    }
  }

}

/**
 * Your FindElements object will be instantiated and called as such:
 * FindElements obj = new FindElements(root);
 * boolean param_1 = obj.find(target);
 */
```

# 결과
[Link](https://leetcode.com/problems/find-elements-in-a-contaminated-binary-tree/submissions/1550250189/){:target="_blank"}

# 설명
1. 모든 값이 -1로 변환된 이진 트리의 구조가 입력되면 아래의 규칙을 만족하는 값을 가진 이진 트리로 복구하는 객체를 완성하는 문제이다.
- root의 val 값은 0이다.
- treeNode의 값이 x이고 left 노드가 null이 아닌 경우, left 노드의 val 값은 $2 \times x + 1$ 값이 된다.
- treeNode의 값이 x이고 right 노드가 null이 아닌 경우, right 노드의 val 값은 $2 \times x + 2$ 값이 된다.
- 생성자인 FindElements(TreeNode root)는 오염된 객체를 초기화하고 복구한다.
- 메서드인 find(int target)는 복구된 이진 트리에서 target 값이 존재하는지 검증한다.

2. 전역 변수인 bitSet은 비트 단위로 값을 저장하고 해당 값이 존재하는지 여부를 저장할 변수이다.

3. 생성자인 FindElements(TreeNode root)를 완성한다.
- root의 val 값을 0으로 넣어준다.
- bitSet에 값 존재를 검증하기 효율적인 객체인 BitSet으로 초기화한다.
- 4번에서 정의한 bfs(TreeNode node) 메서드를 수행하여 이진 트리를 복구한다.

4. BFS 방식으로 이진 트리를 복구하기 위한 bfs(TreeNode node) 메서드를 정의한다.
- bitSet에 node의 val 값을 넣어준다.
- node의 left 노드가 존재하는 경우, 해당 노드의 val 값에 $(2 \times x) + 1$을 넣어준 후 해당 노드로 재귀 호출을 수행한다.
- node의 right 노드가 존재하는 경우, 해당 노드의 val 값에 $(2 \times x) + 2$을 넣어준 후 해당 노드로 재귀 호출을 수행한다.

5. 메서드인 find(int target)를 완성한다.
- bitSet에서 target 값이 존재하는지 여부를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindElementsInAContaminatedBinaryTree.java){:target="_blank"}에서 확인 가능합니다.