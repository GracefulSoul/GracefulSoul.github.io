---
title: "Leetcode Java Unique Binary Search Trees II"
excerpt: "Leetcode Unique Binary Search Trees II Java 풀이"
last_modified_at: 2021-07-15T17:00:00
header:
  image: /assets/images/leetcode/unique-binary-search-trees-ii.png
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
[Link](https://leetcode.com/problems/unique-binary-search-trees-ii/){:target="_blank"}

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

  public List<TreeNode> generateTrees(int n) {
    return this.recursive(1, n);
  }

  private List<TreeNode> recursive(int start, int end) {
    List<TreeNode> result = new ArrayList<>();
    if (start > end) {
      result.add(null);
    }
    for (int idx = start; idx <= end; idx++) {
      for (TreeNode left : this.recursive(start, idx - 1)) {
        for (TreeNode right : this.recursive(idx + 1, end)) {
          result.add(new TreeNode(idx, left, right));
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/522820317/){:target="_blank"}

# 설명
1. 숫자 n이 주어지면 중복되지 않은 다양한 구성의 [이진 트리](https://en.wikipedia.org/wiki/Binary_tree){:target="_blank"}를 생성하는 문제이다.

2. 재귀호출을 통해 1부터 n까지 값을 가진 중복되지 않은 TreeNode들을 생성한다.
- 결과를 저장할 변수 result를 정의한다.
- start가 end보다 큰 경우 결과가 없으므로, result에 null을 넣어준다.

3. 아래의 반복을 수행하여 중복되지 않은 TreeNode를 만들어 변수 result에 넣어준다.
- start 부터 end까지 반복한다.
- start 부터 $idx - 1$까지 재귀호출을 수행하여 left에 들어갈 TreeNode를 만들어 반복을 수행한다.
- $idx - 1$부터 end까지 재귀호출을 수행하여 right에 들어갈 TreeNode를 만들어 반복을 수행한다.
- 위의 세 반복을 통해 만들어진 idx, left, right를 이용하여 새 TreeNode를 result에 넣어준다.

4. 반복이 완료되면 중복되지 않은 TreeNode를 넣은 변수 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniqueBinarySearchTreesII.java){:target="_blank"}에서 확인 가능합니다.