---
title: "Leetcode Java Leaf-Similar Trees"
excerpt: "Leetcode Leaf-Similar Trees Java"
last_modified_at: 2023-03-13T19:00:00
header:
  image: /assets/images/leetcode/leaf-similar-trees.png
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
[Link](https://leetcode.com/problems/leaf-similar-trees){:target="_blank"}

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

  public boolean leafSimilar(TreeNode root1, TreeNode root2) {
    List<Integer> list1 = new ArrayList<>();
    List<Integer> list2 = new ArrayList<>();
    this.dfs(root1, list1);
    this.dfs(root2, list2);
    if (list1.size() != list2.size()) {
      return false;
    }
    for (int i = 0; i < list1.size(); i++) {
      if (!list1.get(i).equals(list2.get(i))) {
        return false;
      }
    }
    return true;
  }

  private void dfs(TreeNode root, List<Integer> list) {
    if (root != null) {
      if (root.left == null && root.right == null) {
        list.add(root.val);
      } else {
        this.dfs(root.left, list);
        this.dfs(root.right, list);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/leaf-similar-trees/submissions/914341388/){:target="_blank"}

# 설명
1. root1과 root2의 리프 노드의 값의 순서가 동일한지 검증하는 문제이다.

2. list1과 list2는 리프 노드들을 저장할 변수로, 3번에서 정의한 dfs(TreeNode root, List<Integer> list) 메서드를 이용하여 root1의 리프 노드들을 list1에 root2의 리프 노드들을 list2에 저장한다.

3. DFS 방식으로 리프 노드를 순차적으로 저장할 dfs(TreeNode root, List<Integer> list) 메서드를 정의한다.
- root가 null이 아닌 경우, 아래를 수행한다.
  - root의 left TreeNode와 right TreeNode가 null인 리프 노드인 경우, list에 root의 val 값을 넣어준다.
  - 위의 경우가 아니라면 root의 left TreeNode를 이용하여 재귀 호출 후 right TreeNode로 다시 재귀 호출을 수행 한다.

4. root1과 root2의 리프 노드들이 list1과 list2에 저장되었으면, list1과 list2의 길이가 같은지 여부를 우선 검증하여 길이가 다르면, false를 주어진 문제의 결과로 반환한다.

5. list1과 list2의 값의 순서가 동일한지 검증하여 동일하지 않으면 false를, 동일하면 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LeafSimilarTrees.java){:target="_blank"}에서 확인 가능합니다.