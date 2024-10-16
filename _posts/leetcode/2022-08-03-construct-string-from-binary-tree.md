---
title: "Leetcode Java Construct String from Binary Tree"
excerpt: "Leetcode Construct String from Binary Tree Java"
last_modified_at: 2022-08-03T20:00:00
header:
  image: /assets/images/leetcode/construct-string-from-binary-tree.png
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
[Link](https://leetcode.com/problems/construct-string-from-binary-tree/){:target="_blank"}

# 코드
```java
class Solution {

  public String tree2str(TreeNode root) {
    StringBuilder sb = new StringBuilder();
    this.dfs(root, sb);
    return sb.toString();
  }

  private void dfs(TreeNode root, StringBuilder sb) {
    if (null != root) {
      sb.append(root.val);
      if (null != root.left) {
        sb.append('(');
        this.dfs(root.left, sb);
        sb.append(')');
      }
      if (null != root.right) {
        if (null == root.left) {
          sb.append('(').append(')');
        }
        sb.append('(');
        this.dfs(root.right, sb);
        sb.append(')');
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/764093480/){:target="_blank"}

# 설명
1. 이진 트리를 root 노드를 기준으로 Pre Order 순으로 소괄호를 이용한 관계를 문자열로 만들어 반환하는 문제이다.
- 단, 우측 자식 노드가 빈 경우 소괄호로 표시하지 않는다.

2. 조건의 문자열을 동적으로 만들기 위한 sb 변수를 정의한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

3. 4번에서 정의한 dfs(TreeNode root, StringBuilder sb)를 활용하여 sb에 주어진 조건을 만족하는 문자열을 넣어준다.

4. DFS 방식으로 문자열을 생성할 dfs(TreeNode root, StringBuilder sb) 메서드를 정의한다.
- root가 null이면 아무것도 수행하지 않는다.
- sb에 root의 val 값을 넣어준다.
- root의 left 노드가 비어있지 않은 경우, sb에 소괄호 시작 문자를 넣은 후 root의 left 노드를 이용한 재귀 호출을 수행하고 sb에 소괄호의 종료 문자를 넣는다.
- root의 right 노드가 비어있지 않은 경우, root의 left 노드가 비어있으면 sb에 빈 소괄호를 넣어주고 위와 동일하게 sb에 소괄호 시작 문자를 넣은 후 root의 right 노드를 이용한 재귀 호출을 수행하고 sb에 소괄호의 종료 문자를 넣는다.

5. 수행이 완료되면 주어진 문제의 결과로 조건을 만족하는 문자열이 담긴 sb를 문자열로 변환하여 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConstructStringFromBinaryTree.java){:target="_blank"}에서 확인 가능합니다.