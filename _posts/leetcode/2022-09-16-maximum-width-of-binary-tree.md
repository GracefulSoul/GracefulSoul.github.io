---
title: "Leetcode Java Maximum Width of Binary Tree"
excerpt: "Leetcode - 'Maximum Width of Binary Tree' 문제 Java 풀이"
last_modified_at: 2022-09-16T10:30:00
header:
  image: /assets/images/leetcode/maximum-width-of-binary-tree.png
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
[Link](https://leetcode.com/problems/maximum-width-of-binary-tree){:target="_blank"}

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

  public int widthOfBinaryTree(TreeNode root) {
    return this.dfs(root, 0, 0, new HashMap<>(), 1);
  }

  private int dfs(TreeNode treeNode, int level, int max, Map<Integer, Integer> map, int id) {
    if (treeNode == null) {
      return 0;
    } else {
      map.putIfAbsent(level, id);
      max = Math.max(max, id - map.get(level) + 1);
      max = Math.max(max, this.dfs(treeNode.left, level + 1, max, map, 2 * id));
      max = Math.max(max, this.dfs(treeNode.right, level + 1, max, map, 2 * id + 1));
      return max;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/801658943/){:target="_blank"}

# 설명
1. root의 level 별 가장 좌측에 존재하는 노드와 가장 우측에 존재하는 노드 간 길이가 가장 긴 값을 구하는 문제이다.

2. 3번에서 정의한 dfs(TreeNode treeNode, int level, int max, Map<Integer, Integer> map, int id) 메서드에 treeNode엔 root, level과 max엔 0, id는 1을 넣고, map은 HashMap으로 초기화 하여 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 root를 탐색하여 노드 간 최대 길이를 구할 dfs(TreeNode treeNode, int level, int max, Map<Integer, Integer> map, int id) 메서드를 정의한다.
- treeNode가 null인 경우 길이 탐색이 불가능하므로, 0을 반환한다.
- map의 level이 키인 값이 없을 경우, 노드 길이 계산의 시작 위치인 id를 넣는다.
- max에 max와 아래의 수행 결과 중 큰 값을 넣어준다.
  - 현재 노드의 id 값과 해당 level의 노드 시작 id의 차이에 1을 더한 값인 현재 level 내 treeNode의 길이.
  - treeNode의 left TreeNode와 고유 id인 $id \times 2$를 이용하여 재귀 호출하여 수행된 결과.
  - treeNode의 right TreeNode와 고유 id인 $(id \times 2) + 1$를 재귀 호출하여 수행된 결과.
- 수행이 완료되면 가장 긴 길이인 max를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumWidthOfBinaryTree.java){:target="_blank"}에서 확인 가능합니다.