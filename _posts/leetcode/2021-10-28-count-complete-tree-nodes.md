---
title: "Leetcode Java Count Complete Tree Nodes"
excerpt: "Leetcode Count Complete Tree Nodes Java 풀이"
last_modified_at: 2021-10-28T13:00:00
header:
  image: /assets/images/leetcode/count-complete-tree-nodes.png
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
[Link](https://leetcode.com/problems/count-complete-tree-nodes/){:target="_blank"}

# 코드
```java
class Solution {

//  Default
//  public int countNodes(TreeNode root) {
//    return root == null ? 0 : 1 + this.countNodes(root.left) + this.countNodes(root.right);
//  }

  public int countNodes(TreeNode root) {
    int depth = this.getDepth(root);
    if (depth == -1) {
      return 0;
    } else {
      if (this.getDepth(root.right) == depth - 1) {
        return (1 << depth) + this.countNodes(root.right);
      } else {
        return (1 << (depth - 1)) + this.countNodes(root.left);
      }
    }
  }

  private int getDepth(TreeNode root) {
    return root == null ? -1 : 1 + this.getDepth(root.left);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/578424222/){:target="_blank"}

# 설명
1. 주어진 [Complete binary tree(완전 이진 트리)](https://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees){:target="_blank"}, TreeNode인 root를 이용하여 모든 노드의 숫자를 구하는 문제이다.
- 단, O(n) 미만의 시간 복잡도로 풀이하여야 한다.
- 단순히 재귀 호출로 root의 모든 노드를 탐색하여 구하는 주석 처리된 Default의 경우 O(n)의 시간 복잡도이므로 출제된 의도와 상반되게 된다.

2. depth에 root로 재귀 호출을 사용하여 가장 좌측 노드의 최대 depth를 구해 넣는다.
- 완전 이진 트리의 경우 기본적으로 마지막 레벨의 모든 노드는 가능한 왼쪽에 존재하므로, 좌측의 TreeNode를 기준으로 계산한다.

3. depth가 0인 경우, 자식 노드가 없는 경우이므로 0을 반환한다.

4. depth가 0이 아닌경우, root의 right TreeNode를 이용하여 2번에 사용된 방법으로 최대 depth를 계산하고 $depth - 1$과 동일한지 검증한다.
- 높이가 x인 이진 트리의 전체 노드의 숫자는 $2^x - 1$로, 비트 연산으로는 $(1 << x) - 1$로 계산이 가능하므로, 아래의 검증에 활용한다.
- 동일하면 root를 기준으로 우측의 leaf(노드)의 최대 depth가 좌측과 같은 경우이므로, depth까지 노드의 수를 위의 공식으로 계산한 결과에 root의 우측 기준으로 노드를 재귀 호출을 이용하여 모든 노드의 수를 계산한다.
  - 전체 노드의 숫자에 우측 노드가 없는 노드들의 개수를 감소시킨다.
- 동일하지 않으면 root를 기준으로 우측의 leaf(노드)의 최대 depth가 좌측보다 낮은 경우이므로, $depth - 1$까지 노드의 수를 위의 공식으로 계산한 결과에 root의 좌측 기준으로 노드를 재귀 호출을 이용하여 모든 노드의 수를 계산한다.
  - $depth - 1$까지 전체 노드의 숫자에 좌측에 남은 노드들을 센다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountCompleteTreeNodes.java){:target="_blank"}에서 확인 가능합니다.