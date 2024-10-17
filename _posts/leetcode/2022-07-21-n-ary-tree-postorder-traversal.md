---
title: "Leetcode Java N-ary Tree Postorder Traversal"
excerpt: "Leetcode - 'N-ary Tree Postorder Traversal' 문제 Java 풀이"
last_modified_at: 2022-07-21T18:30:00
header:
  image: /assets/images/leetcode/n-ary-tree-postorder-traversal.png
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
[Link](https://leetcode.com/problems/n-ary-tree-postorder-traversal/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> postorder(Node root) {
    List<Integer> result = new ArrayList<>();
    this.dfs(root, result);
    return result;
  }

  private void dfs(Node root, List<Integer> list) {
    if (root != null) {
      if (root.children != null) {
        for (Node node : root.children) {
          this.dfs(node, list);
        }
      }
      list.add(root.val);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/752774473/){:target="_blank"}

# 설명
1. root를 postorder 순으로 val 값들을 반환하는 문제이다.
- 이전 [N-ary Tree Preorder Traversal](../n-ary-tree-preorder-traversal){:target="_blank"}과 유사한 문제로, order를 다르게 반환하는 문제이다.

2. result는 postorder 순으로 val 값을 넣을 변수로, ArrayList로 초기화한다.

3. 4번에서 정의한 dfs(Node root, List<Integer> list)에 result를 넣어 수행한다.

4. root를 postorder 순으로 val 값을 넣기 위한 dfs(Node root, List<Integer> list)를 정의한다
- root가 null이 아닌 경우 아래를 수행한다.
- root의 children이 null이 아닌 경우, children을 순차적으로 root 자리에 넣어 재귀 호출을 한다.
- list의 root의 val 값을 넣어준다.

5. root를 postorder 순으로 val 값들을 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NAryTreePostorderTraversal.java){:target="_blank"}에서 확인 가능합니다.