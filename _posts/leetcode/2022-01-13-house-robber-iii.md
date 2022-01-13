---
title: "Leetcode Java House Robber III"
excerpt: "Leetcode House Robber III Java 풀이"
last_modified_at: 2022-01-13T12:00:00
header:
  image: /assets/images/leetcode/house-robber-iii.png
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
[Link](https://leetcode.com/problems/house-robber-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public int rob(TreeNode root) {
    int[] result = this.recursive(root);
    return Math.max(result[0], result[1]);
  }

  private int[] recursive(TreeNode root) {
    int[] result = new int[2];
    if (root == null) {
      return result;
    }
    int[] left = this.recursive(root.left);
    int[] right = this.recursive(root.right);
    result[0] = root.val + left[1] + right[1];
    result[1] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/618697308/){:target="_blank"}

# 설명
1. 주어진 TreeNode인 root의 최상위 노드부터 시작해서 도둑질할 수 있는 최대 금액을 구하는 문제이다.
- 단, 자식 노드가 두 개인 노드의 금액은 도둑질이 불가능하다.

2. 재귀 호출을 사용하여 root를 순회할 recursive(TreeNode root) 메서드를 완성한다.
- 정수 배열인 result를 최대 자식 노드의 갯수인 2의 크기로 초기화 하여 정의한다.
- root가 null인 경우 더 이상 탐색이 불가능하므로, result를 그대로 반환한다.
- root의 left TreeNode를 재귀 호출한 결과를 left에, right TreeNode를 재귀 호출한 결과를 right에 넣어준다.
- result에 재귀 호출로 구해진 left와 right를 이용하여 두 값을 넣어준다.
  - 첫 번째 값에 $root.val + left[1] + right[1]$을 넣어준다.
  - 두 번째 값에 left[0]과 left[1] 중 큰 값과 right[0]과 right[1] 중 큰 값의 합을 넣어준다.
- result를 반환한다.

3. root를 2번의 재귀 호출을 수행한 결과를 result에 넣어주고, result[0] 과 result[1] 중 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HouseRobberIII.java){:target="_blank"}에서 확인 가능합니다.