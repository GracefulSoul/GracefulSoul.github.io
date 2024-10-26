---
title: "Leetcode Java Height of Binary Tree After Subtree Removal Queries"
excerpt: "Leetcode - 'Height of Binary Tree After Subtree Removal Queries' 문제 Java 풀이"
last_modified_at: 2024-10-26T12:00:00
header:
  image: /assets/images/leetcode/height-of-binary-tree-after-subtree-removal-queries.png
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
[Link](https://leetcode.com/problems/height-of-binary-tree-after-subtree-removal-queries/){:target="_blank"}

# 코드
```java
class Solution {

  private int[] heights;
  private int max;

  public int[] treeQueries(TreeNode root, int[] queries) {
    this.heights = new int[100001];
    this.max = 0;
    this.calculateLeftToRight(root, 0);
    this.max = 0;
    this.calculateRightToLeft(root, 0);
    int length = queries.length;
    int[] result = new int[length];
    for (int i = length - 1; i >= 0; i--) {
      result[i] = this.heights[queries[i]];
    }
    return result;
  }

  private void calculateLeftToRight(TreeNode node, int height) {
    if (node != null) {
      this.heights[node.val] = this.max;
      this.max = Math.max(this.max, height);
      this.calculateLeftToRight(node.left, height + 1);
      this.calculateLeftToRight(node.right, height + 1);
    }
  }

  private void calculateRightToLeft(TreeNode node, int height) {
    if (node != null) {
      this.heights[node.val] = Math.max(this.heights[node.val], this.max);
      this.max = Math.max(this.max, height);
      this.calculateRightToLeft(node.right, height + 1);
      this.calculateRightToLeft(node.left, height + 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/height-of-binary-tree-after-subtree-removal-queries/submissions/1433855345/){:target="_blank"}

# 설명
1. 이진 트리인 root에서 queries 내 각 값에 대한 노드를 제거했을 때 트리의 길이를 각각 구하는 문제이다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- heights는 각 위치 값에 해당하는 노드를 제거하였을 때 길이를 저장할 변수이다.
- max는 root의 가장 긴 높이를 저장한 변수이다.

3. 문제 풀이에 필요한 전역 변수를 초기화한다.
- heights에 값의 상한 값보다 1 큰 $10^5 + 1$ 크기의 정수 배열로 초기화한다.
- max를 0으로 초기화한다.

4. 좌측에서 우측으로 탐색하기 위한 calculateLeftToRight(TreeNode node, int height)를 아래와 같이 정의 후 height에 0을 넣어 수행한다.
- node가 null이 아닌 경우만 계속 진행한다.
- heights 내 node의 val 값에 해당하는 위치에 max 값을 넣어준다.
- max에 이전까지 최대 높이인 max와 현재 위치의 높이인 height 중 큰 값을 넣어준다.
- node의 left 노드와 right 노드를 이용하여 height를 증가시켜 순차적으로 재귀 호출을 수행한다.

5. max를 0으로 초기화하고 우측에서 좌측으로 탐색하기 위한 calculateRightToLeft(TreeNode node, int height)를 아래와 같이 정의 후 height에 0을 넣어 수행한다.
- node가 null이 아닌 경우만 계속 진행한다.
- heights 내 node의 val 값에 해당하는 위치에 해당 위치의 값과 max 값 중 큰 높이를 넣어준다.
- max에 이전까지 최대 높이인 max와 현재 위치의 높이인 height 중 큰 값을 넣어준다.
- node의 right 노드와 left 노드를 이용하여 height를 증가시켜 순차적으로 재귀 호출을 수행한다.

6. result는 결과를 저장할 배열로, queries 길이의 정수 배열로 초기화하여 동일한 위치에 heights 내 queries 값을 꺼내 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HeightOfBinaryTreeAfterSubtreeRemovalQueries.java){:target="_blank"}에서 확인 가능합니다.