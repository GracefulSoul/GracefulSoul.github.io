---
title: "Leetcode Java Largest Local Values in a Matrix"
excerpt: "Leetcode Largest Local Values in a Matrix Java"
last_modified_at: 2024-05-12T12:10:00
header:
  image: /assets/images/leetcode/largest-local-values-in-a-matrix.png
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
[Link](https://leetcode.com/problems/largest-local-values-in-a-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] largestLocal(int[][] grid) {
    int[][] result = new int[grid.length - 2][grid.length - 2];
    for (int i = 0; i < result.length; i++) {
      for (int j = 0; j < result.length; j++) {
        int max = 0;
        for (int k = i; k < i + 3; k++) {
          for (int l = j; l < j + 3; l++) {
            max = Math.max(max, grid[k][l]);
          }
        }
        result[i][j] = max;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-local-values-in-a-matrix/submissions/1255716721/){:target="_blank"}

# 설명
1. grid에서 $3 \times 3$ 범위 내 가장 큰 값으로 이루어진 새 배열을 만들어 반환하는 문제이다.

2. result는 결과를 저장할 변수로, grid보다 가로와 세로가 2 작은 크기의 2차원 배열로 초기화한다.

3. 0부터 result의 길이 이전까지 i와 j를 증가시키며 아래를 반복한다.
- max는 최댓값을 저장할 변수로, 0으로 초기화한다.
- k는 i부터 $i + 3$까지, l은 j부터 $j + 3$까지 k와 l을 증가시키며 아래를 반복하여 max에 $3 \times 3$ 범위 내 가장 큰 값을 넣어준다.
- result[i][j]에 max를 넣어준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestLocalValuesInAMatrix.java){:target="_blank"}에서 확인 가능합니다.