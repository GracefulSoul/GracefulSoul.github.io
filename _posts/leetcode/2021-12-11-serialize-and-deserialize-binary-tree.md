---
title: "Leetcode Java Serialize and Deserialize Binary Tree"
excerpt: "Leetcode Serialize and Deserialize Binary Tree Java 풀이"
last_modified_at: 2021-12-11T20:00:00
header:
  image: /assets/images/leetcode/serialize-and-deserialize-binary-tree.png
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
[Link](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/){:target="_blank"}

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
class Codec {

  // Encodes a tree to a single string.
  public String serialize(TreeNode root) {
    return this.serialize(root, new StringBuilder()).toString();
  }

  private StringBuilder serialize(TreeNode root, StringBuilder stringBuilder) {
    if (root == null) {
      return stringBuilder.append(".");
    }
    stringBuilder.append(root.val).append(",");
    this.serialize(root.left, stringBuilder);
    stringBuilder.append(",");
    this.serialize(root.right, stringBuilder);
    return stringBuilder;
  }

  // Decodes your encoded data to tree.
  public TreeNode deserialize(String data) {
    return this.deserialize(new LinkedList<>(Arrays.asList(data.split(","))));
  }

  private TreeNode deserialize(Queue<String> queue) {
    String val = queue.poll();
    if (".".equals(val)) {
      return null;
    }
    TreeNode root = new TreeNode(Integer.valueOf(val));
    root.left = this.deserialize(queue);
    root.right = this.deserialize(queue);
    return root;
  }

}

// Your Codec object will be instantiated and called as such:
// Codec ser = new Codec();
// Codec deser = new Codec();
// TreeNode ans = deser.deserialize(ser.serialize(root));
```

# 결과
[Link](https://leetcode.com/submissions/detail/600184741/){:target="_blank"}

# 설명
1. TreeNode를 serialize하고 deserialize하여 원래 TreeNode를 복원하는 Codec 클래스를 완성하는 문제이다.
- 메서드인 serialize(TreeNode root)는 주어진 TreeNode인 root를 문자열로 변경한다.
- 메서드인 deserialize(String data)는 주어진 String인 data는 TreeNode를 문자열로 변경한 값으로, 해당 값을 이용하여 TreeNode로 복원한다.

2. 주어진 메서드인 serialize(TreeNode root)를 완성하기 위해 재귀 호출용 메서드 serialize(TreeNode root, StringBuilder stringBuilder)를 완성한다.
- root가 null인 경우, stringBuilder에 마침표(".")를 넣어준다.
- 그 외의 경우 root.val과 콤마(",")를 순차적으로 넣어준다.
- root의 left TreeNode를 재귀 호출을 이용하여 stringBuilder에 순차적으로 값을 넣어준다.
- root의 left TreeNode의 재귀 호출이 완료되면 콤마(",")를 넣어 값을 구분해준다.
- root의 right TreeNode를 재귀 호출을 이용하여 stringBuilder에 순차적으로 값을 넣어준다.
- 위의 수행 결과로 완성된 stringBuilder를 반환한다.

3. 주어진 메서드인 serialize(TreeNode root)를 완성한다.
- 2번에서 만든 serialize(TreeNode root, StringBuilder stringBuilder)를 주어진 TreeNode인 root와 새 StringBuilder 클래스를 생성하여 수행한 결과를 문자열로 치환하여 반환한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

4. 주어진 메서드인 deserialize(String data)를 완성하기 위해 재귀 호출용 메서드 deserialize(Queue<String> queue)를 완성한다.
- queue에서 값을 꺼내 지역 변수 val에 넣어준다.
- val 값이 마침표(".")인 경우 null인 TreeNode이므로, null을 반환한다.
- val 값을 정수형으로 변경하여 새 TreeNode를 root로 정의한다.
- root의 left TreeNode에 queue를 이용한 재귀 호출 결과인 TreeNode를 넣어준다.
- root의 right TreeNode에 queue를 이용한 재귀 호출 결과인 TreeNode를 넣어준다.
- 위의 수행 결과로 완성된 TreeNode를 반환한다.

5. 주어진 메서드인 deserialize(String data)를 완성한다.
- 4번에서 만든 deserialize(Queue<String> queue)를 data를 콤마(",")로 분리한 배열을 List형으로 변환하여 새 LinkedList로 만들어 수행한 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SerializeAndDeserializeBinaryTree.java){:target="_blank"}에서 확인 가능합니다.