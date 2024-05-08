---
title: "Leetcode Java Path In Zigzag Labelled Binary Tree"
excerpt: "Leetcode Path In Zigzag Labelled Binary Tree Java"
last_modified_at: 2024-05-08T19:50:00
header:
  image: /assets/images/leetcode/path-in-zigzag-labelled-binary-tree.png
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
[Link](https://leetcode.com/problems/path-in-zigzag-labelled-binary-tree/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> pathInZigZagTree(int label) {
    List<Integer> result = new ArrayList<>();
    result.addFirst(label);
    while (label > 1) {
      int depth = (int) (Math.log(label) / Math.log(2));
      label = ((int) Math.pow(2, depth) + ((int) Math.pow(2, depth + 1) - 1 - label)) / 2;
      result.addFirst(label);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/path-in-zigzag-labelled-binary-tree/submissions/1252565174/){:target="_blank"}

# 설명
1. 1부터 크기의 순서가 좌 -> 우, 우 -> 좌로 진행되는 이진 트리 중 root에서 label 값을 순차적인 지그재그 순서로 label이 되는 순차적인 값을 구하는 문제이다.

2. result는 결과를 저장할 변수로, ArrayList로 초기화하고 첫 값에 label을 넣어준다.

3. label이 1 초과일 때 까지 아래를 반복한다.
- depth는 이진 트리의 깊이를 저장할 변수로, label의 자연 로그 값에 2의 자연 로그값을 나눈 정수 값을 넣어준다.
- label에 $2 ^ depth + \frac{(2 ^ (depth + 1) - 1 + label)}{2}$인 이진 트리의 부모 노드의 값을 넣어준다.
  - $(int) Math.pow(2, depth + 1) - 1 - label$의 값은 이진 트리에서 현재 레벨로 끝나는 이진 트리의 노드 수이다.
  - 위의 값을 기반으로 계산한 $2 ^ depth + \frac{(2 ^ (depth + 1) - 1 + label)}{2}$의 값은 현재 레벨의 노드 수이다.

4. 위의 반복을 통해 완성된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PathInZigzagLabelledBinaryTree.java){:target="_blank"}에서 확인 가능합니다.