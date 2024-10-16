---
title: "Leetcode Java Amount of Time for Binary Tree to Be Infected"
excerpt: "Leetcode Amount of Time for Binary Tree to Be Infected Java"
last_modified_at: 2024-01-10T11:00:00
header:
  image: /assets/images/leetcode/amount-of-time-for-binary-tree-to-be-infected.png
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
[Link](https://leetcode.com/problems/amount-of-time-for-binary-tree-to-be-infected){:target="_blank"}

# 코드
```java
class Solution {

  private int amount;

  public int amountOfTime(TreeNode root, int start) {
    this.dfs(root, start);
    return this.amount;
  }

  private int dfs(TreeNode root, int start) {
    if (root == null) {
      return 0;
    }
    int left = this.dfs(root.left, start);
    int right = this.dfs(root.right, start);
    if (root.val == start) {
      this.amount = Math.max(left, right);
      return -1;
    } else if (left >= 0 && right >= 0) {
      return Math.max(left, right) + 1;
    } else {
      this.amount = Math.max(this.amount, Math.abs(left - right));
      return Math.min(left, right) - 1;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/amount-of-time-for-binary-tree-to-be-infected/submissions/1141976701/){:target="_blank"}

# 설명
1. root의 감염 시작점인 start부터 모든 노드가 감염되기까지의 시간을 계산하는 문제이다.

2. amount는 감염에 걸리기까지 시간을 저장할 전역 변수이다.

3. 4번에서 정의한 dfs(TreeNode root, int start) 메서드를 수행한 후 amount를 주어진 문제의 결과로 반환한다.

4. DFS 방식으로 감염 시간을 계산하기 위한 dfs(TreeNode root, int start) 메서드를 정의한다.
- root가 null이면 감염 대상이 없으므로, 0을 반환한다.
- left와 right에 각 노드 별 재귀 호출을 수행한 결과를 넣어준다.
- root의 val 값이 start인 감염 시작점인 경우 amount에 left와 right 중 가장 큰 값을 넣어준 후 -1을 반환한다.
- left와 right가 0보다 큰 감염 노드를 포함하지 않은 경우, left와 right의 가장 오래걸리는 시간에 현재 노드까지 포함하여 1을 추가한 시간을 반환한다.
- 위의 경우가 아닌 감염 노드를 포함한 경우, amount에 amount와 $left - right$의 절댓값 중 큰 값을 넣은 후 left와 right 중 작은 값에 1을 뺀 값을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AmountOfTimeForBinaryTreeToBeInfected.java){:target="_blank"}에서 확인 가능합니다.