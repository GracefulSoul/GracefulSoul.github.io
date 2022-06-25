---
title: "Leetcode Java Diameter of Binary Tree"
excerpt: "Leetcode Diameter of Binary Tree Java"
last_modified_at: 2022-06-25T13:00:00
header:
  image: /assets/images/leetcode/diameter-of-binary-tree.png
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
[Link](https://leetcode.com/problems/diameter-of-binary-tree/){:target="_blank"}

# 코드
```java
class Solution {

  public int diameterOfBinaryTree(TreeNode root) {
    int[] result = new int[1];
    this.dfs(root, result);
    return result[0];
  }

  private int dfs(TreeNode root, int[] result) {
    if (root == null) {
      return -1;
    } else {
      int left = this.dfs(root.left, result);
      int right = this.dfs(root.right, result);
      result[0] = Math.max(result[0], left + right + 2);
      return Math.max(left + 1, right + 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/730480177/){:target="_blank"}

# 설명
1. root의 노드들 간 가장 긴 이동 거리(지름)를 구하는 문제이다.

2. 결과를 저장할 result를 1크기의 정수 배열로 정의한다.
- Primitive Type인 int형의 초기값은 0이므로 그대로 사용한다.
- 전역 변수가 아닌 생성된 객체를 활용하여 결과를 탐색하기 위해 배열을 생성하여 해당 내 값을 활용한다.

3. 4번에서 정의한 dfs(TreeNode root, int[] result) 메서드를 수행한다.

4. 노드 간 가장 긴 이동거리를 계산하기 위한 dfs(TreeNode root, int[] result) 메서드를 정의한다.
- root가 null인 경우, -1을 반환하여 이전 거리까지만 계산한다.
- left에 root의 left TreeNode로 재귀 호출한 결과를, right에 root의 right TreeNode로 재귀 호출한 결과를 넣어준다.
- result의 첫 값에 해당 값과 $left + right + 2$의 값 중 큰 값을 넣어준다.
- $left + 1$과 $right + 1$ 중 가장 거리가 긴 값을 반환한다.

5. 수행이 완료되면 노드들 간 가장 긴 이동 거리를 저장한 result 내 첫 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DiameterOfBinaryTree.java){:target="_blank"}에서 확인 가능합니다.