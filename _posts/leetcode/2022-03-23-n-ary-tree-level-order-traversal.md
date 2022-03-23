---
title: "Leetcode Java N-ary Tree Level Order Traversal"
excerpt: "Leetcode N-ary Tree Level Order Traversal Java 풀이"
last_modified_at: 2022-03-23T13:00:00
header:
  image: /assets/images/leetcode/n-ary-tree-level-order-traversal.png
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
[Link](https://leetcode.com/problems/n-ary-tree-level-order-traversal/){:target="_blank"}

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
	public List<List<Integer>> levelOrder(Node root) {
		List<List<Integer>> list = new ArrayList<>();
		if (root != null) {
			this.recursive(root, list, 0);
		}
		return list;
	}

	private void recursive(Node root, List<List<Integer>> list, int level) {
		if (list.size() <= level) {
			list.add(new ArrayList<>());
		}
		list.get(level).add(root.val);
		for (Node node : root.children) {
			this.recursive(node, list, level + 1);
		}
	}
}
```

# 결과
[Link](https://leetcode.com/submissions/detail/665501111/){:target="_blank"}

# 설명
1. 주어진 Node가 주어지면 level 별 val 값을 묶어서 반환하는 문제이다.

2. 결과를 담을 List인 list를 ArrayList로 초기화한다.

3. root가 null이 아닌 경우 4번에서 정의한 recursive(Node root, List<List<Integer>> list, int level) 메서드를 level 0으로 수행한다.

4. 재귀 호출을 이용하여 list에 level 별 노드의 val 값을 넣을 recursive(Node root, List<List<Integer>> list, int level) 메서드를 정의한다.
- list의 크기가 level 이하인 경우, list에 새 ArrayList를 넣어준다.
- list의 level번째 List를 가져와 root의 val 값을 넣어준다.
- root의 children을 반복하여 재귀 호출을 $level + 1$로 수행한다.

5. 결과를 넣은 list를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NaryTreeLevelOrderTraversal.java){:target="_blank"}에서 확인 가능합니다.