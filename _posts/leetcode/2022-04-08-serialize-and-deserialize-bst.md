---
title: "Leetcode Java Serialize and Deserialize BST"
excerpt: "Leetcode Serialize and Deserialize BST Java 풀이"
last_modified_at: 2022-04-08T13:00:00
header:
  image: /assets/images/leetcode/serialize-and-deserialize-bst.png
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
[Link](https://leetcode.com/problems/serialize-and-deserialize-bst/){:target="_blank"}

# 코드
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Codec {

  // Encodes a tree to a single string.
  public String serialize(TreeNode root) {
    StringBuilder sb = new StringBuilder();
    this.serialize(sb, root);
    return sb.toString();
  }

  private void serialize(StringBuilder sb, TreeNode root) {
    if (root != null) {
      sb.append((char) (root.val + '0'));
      this.serialize(sb, root.left);
      this.serialize(sb, root.right);
    }
  }

  // Decodes your encoded data to tree.
  public TreeNode deserialize(String data) {
    TreeNode root = null;
    for (char c : data.toCharArray()) {
      root = this.add(root, c - '0');
    }
    return root;
  }

  private TreeNode add(TreeNode root, int val) {
    if (root == null) {
      return new TreeNode(val);
    } else {
      if (val < root.val) {
        root.left = this.add(root.left, val);
      } else {
        root.right = this.add(root.right, val);
      }
      return root;
    }
  }

}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// String tree = ser.serialize(root);
// TreeNode ans = deser.deserialize(tree);
// return ans;
```

# 결과
[Link](https://leetcode.com/submissions/detail/676073207/){:target="_blank"}

# 설명
1. 이진 검색 트리(BST)를 직렬화, 역직렬화를 수행하는 Codec 클래스를 완성하는 문제이다.
- 메서드인 serialize(TreeNode root)는 주어진 root를 문자열로 직렬화하는 기능을 수행한다.
- 메서드인 deserialize(String data)는 주어진 data를 TreeNode로 역직렬화하는 기능을 수행한다.

2. serialize(TreeNode root) 메서드를 완성한다.
- root를 직렬화 하여 저장할 변수 sb를 정의하고, StringBuilder로 초기화한다.
- 3번에서 정의한 serialize(StringBuilder sb, TreeNode root) 메서드를 이용하여 root를 직렬화한 값을 sb에 넣어준다.
- 직렬화된 값이 저장된 sb를 문자열로 변환하여 반환한다.

3. root를 재귀 호출을 이용하여 직렬화 하는 serialize(StringBuilder sb, TreeNode root) 메서드를 완성한다.
- root가 null이 아닐 경우 아래를 수행한다.
  - sb에 root의 val 값을 문자로 치환하여 넣어준다.
  - left를 이용하여 재귀 호출을 수행하여 sb에 좌측 TreeNode들의 val 값을 직렬화 하여 넣어준다.
  - right를 이용하여 재귀 호출을 수행하여 sb에 우측 TreeNode들의 val 값을 직렬화 하여 넣어준다.

4. deserialize(String data) 메서드를 완성한다.
- data를 TreeNode로 변환하기 위한 root를 정의한다.
- data의 각 문자를 반복하여 5번에서 정의한 add(TreeNode root, int val) 메서드로 역직렬화를 수행하여 root에 넣어준다.
- 반복이 완료되면 역직렬화된 root를 반환한다.

5. root에 val 값을 이용하여 TreeNode를 완성하기 위한 add(TreeNode root, int val) 메서드를 완성한다.
- root가 null인 경우 최상위 노드이므로, val을 이용하여 새 TreeNode를 만들어 반환한다.
- root가 null이 아닌 경우 아래를 수행한다.
  - val 값이 root의 val 미만인 경우 해당 노드 좌측에 위치한 노드이므로, root의 left에 root의 left와 val을 이용한 값을 재귀 호출한 결과를 넣어준다.
  - val 값이 root의 val 이상인 경우 해당 노드 우측에 위치한 노드이므로, root의 right에 root의 right와 val을 이용한 값을 재귀 호출한 결과를 넣어준다.
  - 위의 수행이 완료되면 root를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SerializeAndDeserializeBST.java){:target="_blank"}에서 확인 가능합니다.