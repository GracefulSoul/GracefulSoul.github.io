---
title: "Leetcode Java Smallest Subtree with all the Deepest Nodes"
excerpt: "Leetcode Smallest Subtree with all the Deepest Nodes Java"
last_modified_at: 2023-03-07T19:30:00
header:
  image: /assets/images/leetcode/smallest-subtree-with-all-the-deepest-nodes.png
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
[Link](https://leetcode.com/problems/smallest-subtree-with-all-the-deepest-nodes){:target="_blank"}

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

	public TreeNode subtreeWithAllDeepest(TreeNode root) {
		if (root == null) {
			return null;
		}
		int left = this.getDepth(root.left);
		int right = this.getDepth(root.right);
		if (left > right) {
			return this.subtreeWithAllDeepest(root.left);
		} else if (left < right) {
			return this.subtreeWithAllDeepest(root.right);
		} else {
			return root;
		}
	}

	private int getDepth(TreeNode root) {
		if (root == null) {
			return 0;
		} else {
			return Math.max(this.getDepth(root.left), this.getDepth(root.right)) + 1;
		}
	}

}
```

# 결과
[Link](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/submissions/910084313/){:target="_blank"}

# 설명
1. root에서 가장 깊은 길이를 가진 TreeNode를 모두 포함한 가장 작은 하위 TreeNode를 반환하는 문제이다.

2. root가 null이면 null을 반환한다.

3. left와 right에 4번에서 정의한 getDepth(TreeNode root) 메서드를 각각 left와 right TreeNode를 이용하여 수행한 결과를 넣어준다.

4. 깊이를 계산할 getDepth(TreeNode root) 메서드를 정의한다.
- root가 null이면 0을, 아니면 root의 left와 right TreeNode를 이용하여 재귀 호출 한 결과 중 큰 값을 반환한다.

5. left와 right의 값에 따라 아래를 주어진 문제의 결과로 반환한다.
- left가 right보다 크면 left TreeNode에만 가장 깊은 노드가 존재하므로, root의 left TreeNode를 이용하여 재귀 호출한 결과를 반환한다.
- right가 left보다 크면 right TreeNode에만 가장 깊은 노드가 존재하므로, root의 right TreeNode를 이용하여 재귀 호출한 결과를 반환한다.
- left와 right가 동일한 경우 모두 포함되는 경우는 root밖에 없으므로 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SmallestSubtreeWithAllTheDeepestNodes.java){:target="_blank"}에서 확인 가능합니다.