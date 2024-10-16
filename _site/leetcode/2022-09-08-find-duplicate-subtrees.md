---
title: "Leetcode Java Find Duplicate Subtrees"
excerpt: "Leetcode Find Duplicate Subtrees Java"
last_modified_at: 2022-09-08T19:30:00
header:
  image: /assets/images/leetcode/find-duplicate-subtrees.png
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
[Link](https://leetcode.com/problems/find-duplicate-subtrees){:target="_blank"}

# 코드
```java
class Solution {

  public List<TreeNode> findDuplicateSubtrees(TreeNode root) {
    List<TreeNode> result = new ArrayList<>();
    this.dfs(root, new HashMap<>(), result);
    return result;
  }

  private String dfs(TreeNode treeNode, Map<String, Integer> map, List<TreeNode> result) {
    if (treeNode == null) {
      return ".";
    }
    String subTree = new StringBuilder()
        .append(treeNode.val)
        .append(",")
        .append(this.dfs(treeNode.left, map, result))
        .append(",")
        .append(this.dfs(treeNode.right, map, result))
        .toString();
    map.put(subTree, map.getOrDefault(subTree, 0) + 1);
    if (map.get(subTree) == 2) {
      result.add(treeNode);
    }
    return subTree;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/794641421/){:target="_blank"}

# 설명
1. root 내 중복된 TreeNode를 반환하는 문제이다.

2. 결과를 넣을 result를 정의하고, ArrayList로 초기화한다.
- 3번에서 정의한 dfs(TreeNode treeNode, Map<String, Integer> map, List<TreeNode> result) 메서드에 root와 새 HashMap, result를 넣고 수행한다.

3. DFS preorder로 탐색을 수행할 dfs(TreeNode treeNode, Map<String, Integer> map, List<TreeNode> result) 메서드를 정의한다.
- treeNode가 null인 경우 임의 값인, "."를 반환한다.
- subTree에 아래를 순차적으로 넣은 StringBuilder를 문자열로 변환하여 넣어준다.
  - treeNode.val와 ","를 순차적으로 넣어준다.
  - treeNode의 left TreeNode를 이용하여 재귀 호출을 수행한 결과를 넣고 ","를 넣어준다.
  - 마지막으로 treeNode의 right TreeNode를 이용하여 재귀 호출을 수행한 결과를 넣어준다.
- map의 subTree에 해당하는 값이 있으면 가져오고, 없으면 0을 가져와 1을 더한 값을 다시 map의 subTree에 해당하는 값에 넣어준다.
- 만일 map의 subTree번째 값이 2인 경우 중복된 subTree이므로, result에 subTree를 넣어준다.
- 수행이 완료되면 subTree를 반환한다.

4. 모든 중복된 subTree의 preorder 값들을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindDuplicateSubtrees.java){:target="_blank"}에서 확인 가능합니다.