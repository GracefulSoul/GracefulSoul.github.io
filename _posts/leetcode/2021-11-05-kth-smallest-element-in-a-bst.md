---
title: "Leetcode Java Kth Smallest Element in a BST"
excerpt: "Leetcode Kth Smallest Element in a BST Java 풀이"
last_modified_at: 2021-11-05T09:00:00
header:
  image: /assets/images/leetcode/kth-smallest-element-in-a-bst.png
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
[Link](https://leetcode.com/problems/kth-smallest-element-in-a-bst/){:target="_blank"}

# 코드
```java
class Solution {

  public int kthSmallest(TreeNode root, int k) {
    Stack<TreeNode> stack = new Stack<>();
    while (root != null) {
      stack.push(root);
      root = root.left;
    }
    while (k != 0) {
      TreeNode n = stack.pop();
      if (--k == 0) {
        return n.val;
      }
      TreeNode right = n.right;
      while (right != null) {
        stack.push(right);
        right = right.left;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/582204311/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root에서 k번째로 작은 값을 찾는 문제이다.
- root의 자식 노드들 순차적으로 넣을 stack을 정의한다.

2. root가 null이 되기 전까지 root를 넣고, root에 root의 left Treenode를 넣어준다.

3. k가 0이 아닐 때 까지 반복하여 k번째로 작은 값을 찾는다.
- stack에서 최근 넣은 TreeNode를 꺼내 지역 변수 n에 넣어준다.
- k를 감소시킨 값이 0인 경우 n의 val 값이 k번째로 작은 값이므로, n.val의 값을 주어진 문제의 결과로 반환한다.
- n의 right TreeNode를 지역 변수 right에 넣어준다.
- right가 null이 아닐 때 까지 반복하여 stack에 right를 넣고, 다음으로 right에 right의 left TreeNode를 넣어준다.

4. 반복이 완료되면 해당 값이 존재하지 않으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KthSmallestElementInABST.java){:target="_blank"}에서 확인 가능합니다.