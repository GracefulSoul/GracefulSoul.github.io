---
title: "Leetcode Java Verify Preorder Serialization of a Binary Tree"
excerpt: "Leetcode Verify Preorder Serialization of a Binary Tree Java 풀이"
last_modified_at: 2022-01-08T15:00:00
header:
  image: /assets/images/leetcode/verify-preorder-serialization-of-a-binary-tree.png
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
[Link](https://leetcode.com/problems/verify-preorder-serialization-of-a-binary-tree/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isValidSerialization(String preorder) {
    char[] nodes = preorder.toCharArray();
    int slots = 1;
    for (int idx = 0; idx < nodes.length; idx++) {
      if (nodes[idx] == ',') {
        --slots;
        if (slots < 0) {
          return false;
        }
        if (nodes[idx - 1] != '#') {
          slots += 2;
        }
      }
    }
    slots = (nodes[nodes.length - 1] == '#') ? slots - 1 : slots + 1;
    return slots == 0;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/615326509/){:target="_blank"}

# 설명
1. 주어진 문자열 preorder는 TreeNode의 값들과 Null인 Node는 "#" 문자열을 사용하여 사전 정렬(preorder) 순으로 콤마(,)로 구분하여 넣은 값으로, 해당 문자열이 유효한 TreeNode로 구성되었는지를 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- Nodes는 preorder의 값들을 문자 별 분리하여 저장할 배열이다.
- slots는 preorder를 이용하여 유효한 TreeNode인지를 검증하기 위한 변수로, 1로 초기화 한다.

3. nodes를 순회하여 검증을 수행한다.
- nodes의 idx번째 값이 콤마(",")인 경우, 아래를 수행한다.
  - slots를 감소시켜준다.
  - 만일 slots가 0보다 작아지는 경우 유효한 TreeNode가 될 수 없으므로, false를 주어진 문제의 결과로 반환한다.
  - nodes의 $idx - 1$번째 값이 "#" 문자가 아닌 경우 노드가 존재한다는 의미이므로, slots를 2 증가 시켜준다.

4. 반복이 완료되면 nodes의 마지막 값이 #이면 slots를 1 감소시키고, 아닌 경우 1을 증가시킨다.

5. slots가 0이면 각 값들이 유효한 위치에 존재한다는 의미이므로, 해당 검증 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/VerifyPreorderSerializationOfABinaryTree.java){:target="_blank"}에서 확인 가능합니다.