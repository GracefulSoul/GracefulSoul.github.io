---
title: "Leetcode Java Sum of Left Leaves"
excerpt: "Leetcode - 'Sum of Left Leaves' 문제 Java 풀이"
last_modified_at: 2022-03-04T17:00:00
header:
  image: /assets/images/leetcode/sum-of-left-leaves.png
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
[Link](https://leetcode.com/problems/sum-of-left-leaves/){:target="_blank"}

# 코드
```java
class Solution {

  public int sumOfLeftLeaves(TreeNode root) {
    return this.recursive(root, false);
  }

  private int recursive(TreeNode root, boolean isLeft) {
    if (root == null) {
      return 0;
    } else {
      if (root.left == null && root.right == null) {
        return isLeft ? root.val : 0;
      } else {
        return this.recursive(root.left, true) + this.recursive(root.right, false);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/653095449/){:target="_blank"}

# 설명
1. 주어진 이진 트리인 root의 좌측 노드의 합을 계산하는 문제이다.

2. 3번에서 정의한 recursive(TreeNode root, boolean isLeft) 메서드의 결과를 주어진 문제의 결과로 반환한다.

3. 재귀 호출을 이용하여 root의 좌측 노드의 합만 계산하기 위한 recursive(TreeNode root, boolean isLeft) 메서드를 정의한다.
- root가 null인 경우 좌측 노드가 없으므로, 0을 반환한다.
- root가 null이 아닌 경우, 아래를 수행한다.
  - root의 left와 right 노드가 없을 경우, 해당 노드가 left 노드인 경우 root의 val 값을 아니면 0을 반환한다.
  - root의 left 혹은 right 노드가 있을 경우, root의 left와 right 노드를 각각 재귀 호출 수행하여 합한 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfLeftLeaves.java){:target="_blank"}에서 확인 가능합니다.