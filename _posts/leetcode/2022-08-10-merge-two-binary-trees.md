---
title: "Leetcode Java Merge Two Binary Trees"
excerpt: "Leetcode Merge Two Binary Trees Java"
last_modified_at: 2022-08-10T18:00:00
header:
  image: /assets/images/leetcode/merge-two-binary-trees.png
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
[Link](https://leetcode.com/problems/merge-two-binary-trees/){:target="_blank"}

# 코드
```java
class Solution {

  public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
    if (root1 == null) {
      return root2;
    }
    if (root2 == null) {
      return root1;
    }
    root1.val += root2.val;
    root1.left = this.mergeTrees(root1.left, root2.left);
    root1.right = this.mergeTrees(root1.right, root2.right);
    return root1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/770067658/){:target="_blank"}

# 설명
1. root1과 root2의 두 이진 트리를 합치는 문제이다.

2. 합칠 노드가 없는 두 경우를 먼저 확인한다.
- root1이 null인 경우 root2와 합칠 이진 트리가 없으므로, root2를 주어진 문제의 결과로 반환한다.
- root2가 null인 경우 root1과 합칠 이진 트리가 없으므로, root1을 주어진 문제의 결과로 반환한다.

4. root1의 val 값에 root2의 val을 더해준다.

5. root1의 left TreeNode에 root1의 left TreeNode와 root2의 left TreeNode를 이용하여 재귀 호출을 수행한 결과를 넣어준다.

6. root1의 right TreeNode에 root1의 lrighteft TreeNode와 root2의 right TreeNode를 이용하여 재귀 호출을 수행한 결과를 넣어준다.

7. root1에 root2를 합쳤으므로, root1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MergeTwoBinaryTrees.java){:target="_blank"}에서 확인 가능합니다.