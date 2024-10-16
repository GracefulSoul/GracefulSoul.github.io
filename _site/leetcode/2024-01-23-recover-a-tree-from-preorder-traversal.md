---
title: "Leetcode Java Recover a Tree From Preorder Traversal"
excerpt: "Leetcode Recover a Tree From Preorder Traversal Java"
last_modified_at: 2024-01-22T18:50:00
header:
  image: /assets/images/leetcode/recover-a-tree-from-preorder-traversal.png
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
[Link](https://leetcode.com/problems/recover-a-tree-from-preorder-traversal){:target="_blank"}

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

  private int index = 0;

  public TreeNode recoverFromPreorder(String traversal) {
    return this.dfs(traversal, 0);
  }

  private TreeNode dfs(String traversal, int depth) {
    int num = 0;
    while (this.index + num < traversal.length() && traversal.charAt(this.index + num) == '-') {
      num++;
    }
    if (num != depth) {
      return null;
    }
    int next = this.index + num;
    while (next < traversal.length() && traversal.charAt(next) != '-') {
      next++;
    }
    int val = Integer.parseInt(traversal.substring(this.index + num, next));
    this.index = next;
    TreeNode root = new TreeNode(val);
    root.left = this.dfs(traversal, depth + 1);
    root.right = this.dfs(traversal, depth + 1);
    return root;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/recover-a-tree-from-preorder-traversal/submissions/1153445603/){:target="_blank"}

# 설명
1. preorder로 깊이를 대시('-') 문자의 갯수로 구분된 문자열 traversal을 이용하여 TreeNode를 구성하는 문제이다.

2. index는 traversal 문자열의 위치를 저장할 전역 변수로, 0으로 초기화한다.

3. 4번에서 정의한 dfs(String traversal, int depth)를 depth에 0을 넣어 수행한 결과를 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 TreeNode를 구성하기 위한 dfs(String traversal, int depth) 메서드를 정의한다.
- num은 대시('-') 문자의 갯수를 저장할 변수로, $index + num$이 traversal의 길이 미만이면서 traversal의 해당 위치의 문자가 '-'일때 까지 num을 증가시키며 대시('-') 문자의 갯수를 저장한다.
- num이 depth가 아닌 경우, 연결된 TreeNode가 아니므로 null을 반환한다.
- next는 다음 숫자의 위치를 저장할 변수로, $index + num$을 넣어 초기화한다.
- 다시 next가 traversal의 길이 미만이면서 대시('-') 문자가 아닐 때 까지 next를 이동시켜준다.
- val에 traversal의 [$index + num$, next] 까지 숫자를 정수로 변환하여 넣어준다.
- root에 val 값을 이용하여 TreeNode를 만들어 넣어준다.
- preorder 순으로 TreeNode를 구성하기 위하여 아래를 순차적으로 수행한다.
  - root의 left TreeNode에 $depth + 1$을 이용하여 재귀 호출한 결과를 넣어준다.
  - root의 right TreeNode에 $depth + 1$을 이용하여 재귀 호출한 결과를 넣어준다.
- 위를 이용하여 만들어진 TreeNode인 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RecoverATreeFromPreorderTraversal.java){:target="_blank"}에서 확인 가능합니다.