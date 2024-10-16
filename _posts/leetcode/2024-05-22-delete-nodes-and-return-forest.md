---
title: "Leetcode Java Delete Nodes And Return Forest"
excerpt: "Leetcode Delete Nodes And Return Forest Java"
last_modified_at: 2024-05-22T20:10:00
header:
  image: /assets/images/leetcode/delete-nodes-and-return-forest.png
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
[Link](https://leetcode.com/problems/delete-nodes-and-return-forest/){:target="_blank"}

# 코드
```java
class Solution {

  public List<TreeNode> delNodes(TreeNode root, int[] to_delete) {
    Set<Integer> set = new HashSet<>();
    for (int value : to_delete) {
      set.add(value);
    }
    List<TreeNode> list = new ArrayList<>();
    if (!set.contains(root.val)) {
      list.add(root);
    }
    this.dfs(root, set, list);
    return list;
  }

  private TreeNode dfs(TreeNode node, Set<Integer> set, List<TreeNode> list) {
    if (node == null) {
      return null;
    }
    node.left = this.dfs(node.left, set, list);
    node.right = this.dfs(node.right, set, list);
    if (set.contains(node.val)) {
      if (node.left != null) {
        list.add(node.left);
      }
      if (node.right != null) {
        list.add(node.right);
      }
      return null;
    }
    return node;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/delete-nodes-and-return-forest/submissions/1264812346/){:target="_blank"}

# 설명
1. root에서 to_delete에 해당하는 값을 가진 노드를 제거하는 문제이다.
- 제거된 노드의 자식 노드는 새 노드로 구분하여 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- set은 제거할 값을 저장할 변수로, to_delete의 값을 넣어준다.
- list는 제거된 노드를 제외한 노드들을 저장할 변수로, ArrayList로 초기화하여 set에 root의 val 값이 존재하지 않으면 list에 root를 먼저 넣어준다.

3. 4번의 dfs(TreeNode node, Set<Integer> set, List<TreeNode> list) 메서드를 수행한다.

4. DFS 방식으로 노드를 확인하여 제거할 dfs(TreeNode node, Set<Integer> set, List<TreeNode> list) 메서드를 정의한다.
- node가 null인 경우, 더 이상 진행이 불가능하므로 null을 반환한다.
- node의 left와 right TreeNode를 순차적으로 각각 자신을 이용하여 재귀 호출 수행한 결과를 각 노드의 위치에 넣어준다.
- set에 node의 val 값이 존재하여 해당 노드가 제거되는 경우, node의 left와 right TreeNode가 null이 아니면 list에 각각 넣어주고 null을 반환한다.
- 수행이 완료된 node를 반환한다.

5. 반복이 완료되면 제거할 값의 노드들을 제거한 TreeNode들이 저장된 list를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DeleteNodesAndReturnForest.java){:target="_blank"}에서 확인 가능합니다.