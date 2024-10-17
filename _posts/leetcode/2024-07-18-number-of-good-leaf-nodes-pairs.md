---
title: "Leetcode Java Number of Good Leaf Nodes Pairs"
excerpt: "Leetcode Medium - 'Number of Good Leaf Nodes Pairs' 문제 Java 풀이"
last_modified_at: 2024-07-18T18:40:00
header:
  image: /assets/images/leetcode/number-of-good-leaf-nodes-pairs.png
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
[Link](https://leetcode.com/problems/number-of-good-leaf-nodes-pairs/){:target="_blank"}

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

  private int result;

  public int countPairs(TreeNode root, int distance) {
    this.result = 0;
    this.dfs(root, distance);
    return this.result;
  }

  private int[] dfs(TreeNode root, int distance) {
    if (root == null) {
      return new int[distance + 1];
    } else if (root.left == null && root.right == null) {
      int[] result = new int[distance + 1];
      result[1]++;
      return result;
    } else {
      int[] left = this.dfs(root.left, distance);
      int[] right = this.dfs(root.right, distance);
      for (int i = 1; i < left.length; i++) {
        for (int j = distance - 1; j >= 0; j--) {
          if (i + j <= distance) {
            this.result += left[i] * right[j];
          }
        }
      }
      int[] result = new int[distance + 1];
      for (int i = result.length - 2; i >= 1; i--) {
        result[i + 1] = left[i] + right[i];
      }
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-good-leaf-nodes-pairs/submissions/1325037253/){:target="_blank"}

# 설명
1. 이진 트리 노드인 root의 리프 노드에서 root 노드까지 distance 이하만큼의 거리를 가진 좋은 노드 쌍을 찾는 문제이다.

2. 전역 변수인 result는 리프 노드 쌍을 계산할 변수로, 0으로 초기화한다.

3. 4번에서 정의한 dfs(TreeNode root, int distance) 메서드를 수행해준다.

4. DFS 방식으로 리프 노드 쌍을 탐색할 dfs(TreeNode root, int distance)를 정의한다.
- root가 null인 탐색이 불가능한 경우, $distance + 1$ 크기의 빈 배열을 반환한다.
- root의 자식 노드가 없는 경우, $distance + 1$ 크기의 배열에 두 번째 값만 증가시킨 후 해당 배열을 반환한다.
- 위의 모든 경우가 아닌 경우, 아래를 수행한다.
  - left와 right에 각 자식 노드를 이용하여 재귀 호출한 결과를 넣어준다.
  - 1부터 left 길이 미만까지 i를 증가시키며, $distance - 1$부터 0 이상 까지 j를 감소시키며 전역 변수인 result에 좋은 노드 쌍의 갯수인 $left[i] \times right[j]$의 값을 더해준다.
  - 위의 수행이 완료되면 $distance + 1$ 크기의 정수 배열에 역순으로 left와 right의 처음부터 값의 합을 넣어준 후 해당 배열을 반환한다.

5. 4번의 수행이 완료되면 좋은 노드 쌍이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfGoodLeafNodesPairs.java){:target="_blank"}에서 확인 가능합니다.