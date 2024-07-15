---
title: "Leetcode Java Create Binary Tree From Descriptions"
excerpt: "Leetcode Create Binary Tree From Descriptions Java"
last_modified_at: 2024-07-14T23:30:00
header:
  image: /assets/images/leetcode/create-binary-tree-from-descriptions.png
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
[Link](https://leetcode.com/problems/create-binary-tree-from-descriptions/){:target="_blank"}

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

  public TreeNode createBinaryTree(int[][] descriptions) {
    Map<Integer, TreeNode> map = new HashMap<>();
    Set<Integer> children = new HashSet<>();
    for (int[] description : descriptions) {
      int parent = description[0];
      int child = description[1];
      int isLeft = description[2];
      children.add(child);
      TreeNode node = map.getOrDefault(parent, new TreeNode(parent));
      if (isLeft == 1) {
        node.left = map.getOrDefault(child, new TreeNode(child));
        map.put(child, node.left);
      } else {
        node.right = map.getOrDefault(child, new TreeNode(child));
        map.put(child, node.right);
      }
      map.put(parent, node);
    }
    for (int[] description : descriptions) {
      if (!children.contains(description[0])) {
        return map.get(description[0]);
      }
    }
    return null;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/create-binary-tree-from-descriptions/submissions/1321865111/){:target="_blank"}

# 설명
1. 2차원 정수 배열인 descriptions가 주어지면 아래의 규칙에 따라 TreeNode를 만들어 반환하는 문제이다.
- descriptions[i] = [parent<sub>i</sub>, child<sub>i</sub>, isLeft<sub>i</sub>] 를 만족한다.
- TreeNode 내 parent<sub>i</sub>는 child<sub>i</sub>의 고유한 부모를 나타낸다.
- isLeft<sub>i</sub>가 1이면 부모 노드의 좌측, 0이면 부모 우측 노드임을 나타낸다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 각 값에 대한 노드를 저장할 변수로, HashMap으로 초기화한다.
- children은 각 값들이 자식 노드에 대한 값인지 저장할 변수로, 중복을 제거하기 위하여 HashSet으로 초기화한다.

3. descriptions의 각 값들을 description에 순차적으로 넣어 아래를 수행한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - parent, child, isLeft에 description의 각 값들을 순서대로 넣어준다.
  - node는 부모 노드를 저장할 변수로, map에서 parent에 해당하는 노드를 꺼내 넣어주고, 존재하지 않으면 새 TreeNode를 parent 값으로 초기화하여 넣어준다.
- children에 child를 넣어 자식 노드의 값을 추가해준다.
- isLeft가 1이면 node의 left에, 0이면 node의 right에 map에서 child에 해당하는 노드가 존재하면 꺼내 넣어주고, 존재하지 않으면 새 TreeNode를 child 값으로 초기화하여 넣어 준다.
- 위의 각 경우에 따른 node를 map 내 child의 값으로 저장시켜준다.
- map 내 parent의 값으로 node를 저장시켜준다.

4. 위의 반복이 완료되면 다시 descriptions 내 각 배열들의 첫 번째 값이 children에 존재하지 않은 값을 찾아 map에서 해당 노드를 찾아 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CreateBinaryTreeFromDescriptions.java){:target="_blank"}에서 확인 가능합니다.