---
title: "Leetcode Java Path Sum III"
excerpt: "Leetcode Path Sum III Java 풀이"
last_modified_at: 2022-03-29T13:00:00
header:
  image: /assets/images/leetcode/path-sum-iii.png
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
[Link](https://leetcode.com/problems/path-sum-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public int pathSum(TreeNode root, int targetSum) {
    if (root == null) {
      return 0;
    } else {
      Map<Integer, Integer> map = new HashMap<>();
      map.put(0, 1);
      return this.dfs(root, targetSum, map, 0);
    }
  }

  private int dfs(TreeNode node, int targetSum, Map<Integer, Integer> map, int sum) {
    int result = 0;
    sum += node.val;
    if (map.containsKey(sum - targetSum)) {
      result += map.get(sum - targetSum);
    }
    map.put(sum, map.getOrDefault(sum, 0) + 1);
    if (node.left != null) {
      result += this.dfs(node.left, targetSum, map, sum);
    }
    if (node.right != null) {
      result += this.dfs(node.right, targetSum, map, sum);
    }
    map.put(sum, map.get(sum) - 1);
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/669405657/){:target="_blank"}

# 설명
1. TreeNode인 root를 이용하여 val의 합이 targetSum이 되는 구간의 개수를 구하는 문제이다.

2. root가 null인지 여부에 따라 아래를 수행한다.
- root가 null인 경우 val의 합이 targetSum이 되는 구간의 개수를 셀 수 없으므로, 0을 주어진 문제의 결과로 반환한다.
- root가 null이 아닌 경우 아래를 수행한다.
  - map에 새 HashMap을 정의하고 키가 1인 값에 1을 넣어 초기화한다.
  - 3번에서 정의한 dfs(TreeNode node, int targetSum, Map<Integer, Integer> map, int sum) 메서드를 sum에 0을 넣어 수행한다.

3. DFS 방식으로 구간의 개수를 세기 위한 dfs(TreeNode node, int targetSum, Map<Integer, Integer> map, int sum) 메서드를 정의한다.
- 개수를 세기 위한 result를 0으로 초기화한다.
- sum에 node의 val 값을 더하여 구간 합을 계산한다.
- map에 $sum - targetSum$의 값이 존재하는 경우, result에 해당 값을 더해준다.
- map에 sum이 키인 값에 기존 값이 있으면 sum 아니면 0에 1을 더해서 넣어 map에 구간 개수를 추가해준다.
- node의 left TreeNode가 null이 아닌 경우, left TreeNode로 재귀 호출하여 좌측으로 탐색한 결과를 result에 더해준다.
- node의 right TreeNode가 null이 아닌 경우, right TreeNode로 재귀 호출하여 우측으로 탐색한 결과를 result에 더해준다.
- map에 sum이 키인 값에 기존 값의 1을 뺀 값을 넣어 앞에서 구간 개수를 추가한 것을 초기화 시켜준다.
- result를 반환하여 node 기준으로 탐색한 targetSum이 되는 구간의 개수를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PathSumIII.java){:target="_blank"}에서 확인 가능합니다.