---
title: "Leetcode Java Binary Tree Paths"
excerpt: "Leetcode Binary Tree Paths Java 풀이"
last_modified_at: 2021-11-19T10:40:00
header:
  image: /assets/images/leetcode/binary-tree-paths.png
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
[Link](https://leetcode.com/problems/binary-tree-paths/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> binaryTreePaths(TreeNode root) {
    List<String> result = new ArrayList<>();
    this.recursive(root, result, new StringBuilder(), 0);
    return result;
  }

  public void recursive(TreeNode root, List<String> list, StringBuilder stringBuilder, int length) {
    if (root == null) {
      return;
    }
    stringBuilder.append(root.val);
    if (root.left == null && root.right == null) {
      list.add(stringBuilder.toString());
    } else {
      stringBuilder.append("->");
      this.recursive(root.left, list, stringBuilder, stringBuilder.length());
      this.recursive(root.right, list, stringBuilder, stringBuilder.length());
    }
    stringBuilder.setLength(length);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/589340307/){:target="_blank"}

# 설명
1. 주어진 이진 트리인 root를 이용하여 root부터 leaf까지 이어진 모든 결과를 반환하는 문제이다.

2. root부터 leaf까지 이어진 모든 결과를 담을 result 컬렉션을 정의한다.

3. StringBuilder를 활용한 재귀 호출을 이용하여 result에 모든 경우의 수를 넣어준다.
- root가 null인 경우 수행이 불가능하므로, 종료한다.
- root의 val 값을 stringBuilder에 넣어 값을 이어준다.
- root의 left와 right TreeNode가 null인 경우 더 이어줄 node가 없으므로, stringBuilder의 결과를 list에 넣어준다.
- 그 외의 경우 stringBuilder에 "->" 키워드를 넣어주고, root의 left와 right TreeNode를 순서대로 재귀 호출 수행한다.
  - 단, stringBuilder의 길이를 각각 넣어준다.
- 수행이 완료되면 stringBuilder에 length 값을 주입하여 length 번째 이후에 등록된 값들을 제거해준다.

4. 재귀 호출이 완료되면 root부터 leaf까지 이어진 모든 결과를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryTreePaths.java){:target="_blank"}에서 확인 가능합니다.