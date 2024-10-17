---
title: "Leetcode Java Maximum Depth of N-ary Tree"
excerpt: "Leetcode - 'Maximum Depth of N-ary Tree' 문제 Java 풀이"
last_modified_at: 2022-07-05T19:30:00
header:
  image: /assets/images/leetcode/maximum-depth-of-n-ary-tree.png
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
[Link](https://leetcode.com/problems/maximum-depth-of-n-ary-tree/){:target="_blank"}

# 코드
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {

  public int maxDepth(Node root) {
    if (root == null) {
      return 0;
    } else {
      int max = 0;
      for (Node children : root.children) {
        max = Math.max(max, this.maxDepth(children));
      }
      return max + 1;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/739033165/){:target="_blank"}

# 설명
1. root의 최대 깊이를 구하는 문제이다.

2. root가 null인 경우 더 이상 내려갈 수 없으므로, 0을 반환한다.

3. max를 0으로 정의하고 root의 children을 반복하여 children을 재귀 호출한 결과와 max 중 큰 값을 max에 넣어준다.

4. 반복이 완료되면 최대 깊이가 저장된 max에 root를 포함해 1을 더해 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumDepthOfNAryTree.java){:target="_blank"}에서 확인 가능합니다.