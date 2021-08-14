---
title: "Leetcode Java Binary Tree Maximum Path Sum"
excerpt: "Leetcode Binary Tree Maximum Path Sum Java 풀이"
last_modified_at: 2021-08-14T11:00:00
header:
  image: /assets/images/leetcode/binary-tree-maximum-path-sum.png
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
[Link](https://leetcode.com/problems/binary-tree-maximum-path-sum/){:target="_blank"}

# 코드
```java
class Solution {

  private int max = Integer.MIN_VALUE;

  public int maxPathSum(TreeNode root) {
    this.recursive(root);
    return max;
  }

  private int recursive(TreeNode node) {
    if (node == null) {
      return 0;
    }
    int left = Math.max(0, this.recursive(node.left));
    int right = Math.max(0, this.recursive(node.right));
    max = Math.max(max, node.val + left + right);
    return node.val + Math.max(left, right);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/538150367/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root를 이용하여 경로 합이 가장 큰 값을 탐색하는 문제이다.

2. bottom-up으로 max값을 찾기 위해서 전역 변수 max을 정의하고, int의 최소값인 Integer.MIN_VALUE로 초기화 한다.

3. 재귀 호출을 이용하여 경로합이 가장 큰 값을 max에 넣어준다.
- node가 null인 경우 해당 노드가 존재하지 않으므로 0을 반환한다.
- node의 left를 재귀 호출을 수행한 값과 0 중 큰 값을 변수 left에 저장한다.
- node의 right를 재귀 호출을 수행한 값과 0 중 큰 값을 변수 left에 저장한다.
- 전역 변수 max와 $node.val + left + rgiht$의 값 중 큰 값을 max에 저장한다.
- 위의 두 변수인 left와 right 값에 사용하기 위한 node.val와 left와 right 중 큰 값의 합을 반환한다.

4. 재귀 호출이 완료되면 전역 변수인 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreeMaximumPathSum.java){:target="_blank"}에서 확인 가능합니다.