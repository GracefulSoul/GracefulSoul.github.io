---
title: "Leetcode Java Smallest String Starting From Leaf"
excerpt: "Leetcode Smallest String Starting From Leaf Java"
last_modified_at: 2023-09-05T19:20:00
header:
  image: /assets/images/leetcode/smallest-string-starting-from-leaf.png
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
[Link](https://leetcode.com/problems/smallest-string-starting-from-leaf){:target="_blank"}

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

  private String str;

  public String smallestFromLeaf(TreeNode root) {
    this.str = null;
    this.dfs(root, new StringBuilder());
    return this.str;
  }

  public void dfs(TreeNode root, StringBuilder sb) {
    if (root != null) {
      char c = (char) (root.val + 97);
      sb.append(c);
      if (root.left == null && root.right == null) {
        String s = sb.reverse().toString();
        if (this.str == null || this.str.compareTo(s) > 0) {
          this.str = s;
        }
        sb.reverse();
      }
      this.dfs(root.left, sb);
      this.dfs(root.right, sb);
      sb.deleteCharAt(sb.length() - 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/smallest-string-starting-from-leaf/submissions/1041108684/){:target="_blank"}

# 설명
1. 영문자 순서 val에 저장된 이진 트리인 root를 이용하여 가장 마지막인 리프 노드부터 루트 노드까지 사전적인 순서가 가장 작은 단어를 구하는 문제이다.

2. 전역변수인 str은 결과를 저장할 변수이다.

3. str을 null로 초기화하고 4번에서 정의한 dfs(TreeNode root, StringBuilder sb) 메서드에 새 StringBuilder를 초기화하여 넣고 수행한다.

4. DFS 방식으로 단어를 완성할 dfs(TreeNode root, StringBuilder sb) 메서드를 정의한다.
- root가 null인 경우, 수행하지 않는다.
- c에 root의 val 값에 영소문자 'a'의 값인 97을 더해 문자로 변환하여 넣어준다.
- sb에 c를 넣고, root의 left와 right가 null인 리프 노드인 경우, 아래를 수행한다.
  - s에 sb의 순서를 역순으로 반전시켜 문자열로 변환한 값을 넣어준다.
  - 전역 변수인 str이 null이거나 str이 s보다 길이가 더 긴 경우, str에 s를 넣어준다.
  - sb를 다시 반전시켜 원래 순서로 전환시켜준다.
- root의 left TreeNode로 재귀 호출을 수행한 후 right TreeNode로 다시 재귀 호출을 수행한다.
- 위의 수행이 완료되면 sb에서 마지막 문자를 제거하여 수행 전 문자열로 전환한다.

5. 반복이 완료되면 결과가 저장된 str을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SmallestStringStartingFromLeaf.java){:target="_blank"}에서 확인 가능합니다.