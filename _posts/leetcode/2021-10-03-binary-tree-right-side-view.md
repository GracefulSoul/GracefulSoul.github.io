---
title: "Leetcode Java Binary Tree Right Side View"
excerpt: "Leetcode Binary Tree Right Side View Java 풀이"
last_modified_at: 2021-10-03T15:00:00
header:
  image: /assets/images/leetcode/binary-tree-right-side-view.png
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
[Link](https://leetcode.com/problems/binary-tree-right-side-view/){:target="_blank"}

# 코드
```java
public class Solution {

  public List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    this.recursive(result, root, 0);
    return result;
  }

  private void recursive(List<Integer> list, TreeNode treeNode, int level) {
    if (treeNode == null) {
      return;
    }
    if (list.size() == level) {
      list.add(treeNode.val);
    }
    this.recursive(list, treeNode.right, level + 1);
    this.recursive(list, treeNode.left, level + 1);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/564910112/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root를 이용하여 top-bottom 순으로 동일 Level 내 가장 우측에 존재하는 TreeNode의 val 값을 List에 넣는 문제이다.

2. 재귀 호출을 이용하여 List에 top-bottom 순으로 동일 Level 내 가장 우측에 존재하는 TreeNode의 val 값을 넣어준다.
- treeNode가 null인 경우 진행이 불가능하므로 반환한다.
- list.size()와 level이 동일한 경우, 해당 TreeNode의 val 값을 List에 넣어준다.
- treeNode.right -> treeNode.left 순으로 재귀 호출을 수행하여 각 Level 내 가장 우측에 존재하는 TreeNode 의 val 값을 넣어준다.

3. 재귀 호출이 완료되면 top-bottom 순으로 동일 Level 내 가장 우측에 존재하는 TreeNode의 val 값을 넣은 List인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreeRightSideView.java){:target="_blank"}에서 확인 가능합니다.