---
title: "Leetcode Java Convert BST to Greater Tree"
excerpt: "Leetcode Convert BST to Greater Tree Java"
last_modified_at: 2022-06-20T19:50:00
header:
  image: /assets/images/leetcode/convert-bst-to-greater-tree.png
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
[Link](https://leetcode.com/problems/convert-bst-to-greater-tree/){:target="_blank"}

# 코드
```java
class Solution {

  private int sum = 0;

  public TreeNode convertBST(TreeNode root) {
    if (root != null) {
      this.convertBST(root.right);
      sum += root.val;
      root.val = sum;
      this.convertBST(root.left);
    }
    return root;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/726655860/){:target="_blank"}

# 설명
1. BST(Binary Search Tree)인 root를 이용하여 Greater Tree로 변환하는 문제이다.
- Greater Tree는 BST의 가장 큰 값(오른쪽 맨 하위 노드)부터 작은 값(왼쪽 맨 하위 노드)까지 순차적인 합을 각 노드의 값으로 가진 TreeNode이다.

2. 현재 위치의 합을 넣을 sum을 0으로 초기화한다.

3. root가 null이 아니면 아래를 수행한다.
- root의 right TreeNode를 이용하여 재귀 호출을 수행한다.
- sum에 root의 val 값을 더해주고, root의 val에 sum을 넣어준다.
- root의 left TreeNode를 이용하여 재귀 호출을 수행한다.

4. 수행이 완료되면 root를 반환한다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConvertBSTToGreaterTree.java){:target="_blank"}에서 확인 가능합니다.