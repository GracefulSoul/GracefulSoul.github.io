---
title: "Leetcode Java Minimum Absolute Difference in BST"
excerpt: "Leetcode Minimum Absolute Difference in BST Java"
last_modified_at: 2022-06-16T20:00:00
header:
  image: /assets/images/leetcode/minimum-absolute-difference-in-bst.png
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
[Link](https://leetcode.com/problems/minimum-absolute-difference-in-bst/){:target="_blank"}

# 코드
```java
class Solution {

  private int min = Integer.MAX_VALUE;

  public int getMinimumDifference(TreeNode root) {
    this.dfs(root, null);
    return this.min;
  }

  private TreeNode dfs(TreeNode root, TreeNode prev) {
    if (root == null) {
      return prev;
    }
    prev = this.dfs(root.left, prev);
    if (prev != null) {
      this.min = Math.min(this.min, Math.abs(root.val - prev.val));
    }
    return this.dfs(root.right, root);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/722799319/){:target="_blank"}

# 설명
1. root에서 root와 leaf의 val 값 차이가 가장 작은 구간의 값을 구하는 문제이다.

2. 최솟값을 넣을 min을 정의하고 정수의 가장 큰 값으로 초기화한다.

3. 4번에서 정의한 dfs(TreeNode root, TreeNode prev) 메서드를 수행한다.

4. root와 leaf의 val 값 차이가 가장 작은 구간의 값을 구할 dfs(TreeNode root, TreeNode prev) 메서드를 정의한다.
- root가 null인 경우 비교가 불가능하므로, prev를 반환한다.
- prev에 root의 left TreeNode와 prev TreeNode를 이용한 재귀 호출 결과를 넣어준다.
- prev가 null이 아니라면 min과 root의 val, prev의 val 차이 값 중 작은 값을 넣어준다.
- pright TreeNode와 root TreeNode를 이용한 재귀 호출 결과를 반환한다.

5. 재귀 호출이 완료되면 root와 leaf의 val 값 차이가 가장 작은 값을 저장한 min을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumAbsoluteDifferenceInBST.java){:target="_blank"}에서 확인 가능합니다.