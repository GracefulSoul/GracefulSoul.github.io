---
title: "Leetcode Java Path Sum II"
excerpt: "Leetcode Path Sum II Java 풀이"
last_modified_at: 2021-08-03T12:00:00
header:
  image: /assets/images/leetcode/path-sum-ii.png
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
[Link](https://leetcode.com/problems/path-sum-ii/){:target="_blank"}

# 코드
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {

  public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
    List<List<Integer>> result = new ArrayList<>();
    this.recursive(root, new ArrayList<>(), result, targetSum);
    return result;
  }

  public void recursive(TreeNode root, List<Integer> temp, List<List<Integer>> result, int targetSum) {
    if (root == null) {
      return;
    }
    temp.add(new Integer(root.val));
    if (root.left == null && root.right == null && targetSum == root.val) {
      result.add(new ArrayList<>(temp));
    }
    this.recursive(root.left, temp, result, targetSum - root.val);
    this.recursive(root.right, temp, result, targetSum - root.val);
    temp.remove(temp.size() - 1);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/532382529/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root의 마지막 노드까지의 val 값들의 합이 targetSum이 되는 줄기들의 val 값의 집합들을 모두 찾는 문제이다.

2. 재귀 호출을 이용하여 targetSum과 동일한지를 검증하고 해당 val 값의 집합을 result에 넣어준다.
- root가 null인 경우 해당 TreeNode가 존재하지 않으므로, return 시킨다.
- temp ArrayList에 root의 val 값을 넣어준다.
- root의 left와 right가 null이면 마지막 노드이므로, $targetSum - root.val$이 0인 경우 result에 temp를 새 ArrayList로 생성하여 넣어준다.
- left와 right TreeNode도 각각 targetSum에 $targetSum - root.val$을 넣어 재귀 호출을 수행하여 각 val 값들의 합이 targetSum이 되는 줄기를 모두 탐색한다.
- 반복이 끝나기 전에 해당 TreeNode의 val 값을 제거해준다.

3. 재귀 호출이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PathSumII.java){:target="_blank"}에서 확인 가능합니다.