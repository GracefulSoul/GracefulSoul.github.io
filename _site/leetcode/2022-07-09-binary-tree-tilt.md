---
title: "Leetcode Java Binary Tree Tilt"
excerpt: "Leetcode Binary Tree Tilt Java"
last_modified_at: 2022-07-09T12:00:00
header:
  image: /assets/images/leetcode/binary-tree-tilt.png
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
[Link](https://leetcode.com/problems/binary-tree-tilt/){:target="_blank"}

# 코드
```java
class Solution {

  private int sum = 0;

  public int findTilt(TreeNode root) {
    this.recursive(root);
    return this.sum;
  }

  private int recursive(TreeNode root) {
    if (root == null) {
      return 0;
    }
    int left = this.recursive(root.left);
    int right = this.recursive(root.right);
    this.sum += Math.abs(left - right);
    return left + right + root.val;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/742182215/){:target="_blank"}

# 설명
1. root의 기울기를 구하는 문제이다.
- 기울기란 좌측 자식 노드 val 값의 합과 우측 자식 노드 val 값의 합을 뺀 값의 절댓값이다.

2. 기울기를 구하기 위한 sum을 전역 변수로 정의하고, 0으로 초기화한다.

3. 4번에서 정의한 recursive(TreeNode root) 메서드를 수행한다.

4. 기울기를 구하기 위한 recursive(TreeNode root) 메서드를 정의한다.
- root가 null인 경우, 0을 반환한다.
- left와 right TreeNode를 이용하여 재귀 호출을 수행하고, left와 right에 결과를 넣어준다.
- sum에 left와 right의 차이에 대한 절댓값을 넣어준다.
- left와 right와 val 합을 반환한다.

5. 재귀 호출이 완료되면 기울기를 저장한 sum을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreeTilt.java){:target="_blank"}에서 확인 가능합니다.