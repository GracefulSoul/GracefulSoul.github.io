---
title: "Leetcode Java Find Mode in Binary Search Tree"
excerpt: "Leetcode Find Mode in Binary Search Tree Java"
last_modified_at: 2022-05-21T23:00:00
header:
  image: /assets/images/leetcode/find-mode-in-binary-search-tree.png
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
[Link](https://leetcode.com/problems/find-mode-in-binary-search-tree/){:target="_blank"}

# 코드
```java
class Solution {

  private int max = 0;
  private int count = 1;
  private TreeNode prev = null;

  public int[] findMode(TreeNode root) {
    List<Integer> list = new ArrayList<>();
    this.dfs(root, list);
    int[] result = new int[list.size()];
    for (int idx = 0; idx < list.size(); idx++) {
      result[idx] = list.get(idx);
    }
    return result;
  }

  public void dfs(TreeNode node, List<Integer> list) {
    if (node == null) {
      return;
    }
    this.dfs(node.left, list);
    if (this.prev != null) {
      if (node.val == this.prev.val) {
        this.count++;
      } else {
        this.count = 1;
      }
    }
    if (this.count > this.max) {
      list.clear();
      list.add(node.val);
      this.max = this.count;
    } else if (this.count == this.max) {
      list.add(node.val);
    }
    this.prev = node;
    this.dfs(node.right, list);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/704065654/){:target="_blank"}

# 설명
1. 중복된 값이 있는 root를 이용하여 가장 많이 반복된 숫자를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 최대 반복 횟수를 저장할 변수로, 0으로 초기화한다.
- count는 현재 숫자의 반복 횟수를 계산할 변수로, 1로 초기화한다.
- prev는 현재 노드를 저장하고 다음 탐색을 진행하기 위한 변수로, null로 초기화한다.

3. 결과를 저장할 list를 ArrayList로 초기화하여 4번에서 정의한 dfs(TreeNode node, List<Integer> list) 메서드를 수행한다.

4. DFS 방식으로 가장 많이 반복된 숫자를 구할 dfs(TreeNode node, List<Integer> list) 메서드를 정의한다.
- node가 null인 경우, 수행을 중지한다.
- node의 left TreeNode를 이용하여 재귀 호출을 수행한다.
- prev가 null이 아닌 경우, node의 val과 prev의 val이 동일하면 count를 증가시키고 아니면 count를 1로 초기화한다.
- count가 max보다 크면 현재 숫자의 반복 횟수가 더 크므로, list를 초기화 후 list에 node의 val 값을 넣어주고 max에 count를 넣어준다.
- count가 max와 동일한 경우 반복 횟수가 동일한 값이므로, list에 node의 val 값을 넣어준다.
- prev에 node를 넣어주고 node의 right TreeNode로 재귀 호출을 수행한다.

5. 위의 수행이 완료되면 list의 값들을 정수 배열에 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindModeInBinarySearchTree.java){:target="_blank"}에서 확인 가능합니다.