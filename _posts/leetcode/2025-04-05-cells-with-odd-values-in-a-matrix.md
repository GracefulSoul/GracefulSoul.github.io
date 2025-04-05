---
title: "Leetcode Java Cells with Odd Values in a Matrix"
excerpt: "Leetcode - 'Cells with Odd Values in a Matrix' 문제 Java 풀이"
last_modified_at: 2025-04-05T11:50:00
header:
  image: /assets/images/leetcode/cells-with-odd-values-in-a-matrix.png
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
[Link](https://leetcode.com/problems/cells-with-odd-values-in-a-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  public int oddCells(int m, int n, int[][] indices) {
    int count = 0;
    int[] rows = new int[m];
    int[] cols = new int[n];
    for (int[] indice : indices) {
      rows[indice[0]]++;
      cols[indice[1]]++;
    }
    for (int row : rows) {
      for (int col : cols) {
        if ((row + col) % 2 != 0) {
          count++;
        }
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/cells-with-odd-values-in-a-matrix/submissions/1597062222/){:target="_blank"}

# 설명
1. 0으로 채워진 $m \times n$ 크기의 정수 배열을 이용하여 아래 규칙을 만족하는 indices를 수행한 결과 중 홀수 값의 갯수를 반환하는 문제이다.
- indices[i] = [r<sub>i</sub>, c<sub>i</sub>]이다.
- r<sub>i</sub>는 i번째 행의 값을 모두 증가시킨다.
- c<sub>i</sub>는 i번째 열의 값을 모두 증가시킨다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 홀수 값의 갯수를 저장할 변수로, 0으로 초기화한다.
- rows와 cols는 각 행과 열의 증가되는 값을 저장할 변수로, m과 n 크기의 정수 배열로 초기화 후 indices를 순차적으로 수행하여 각 증가되는 값을 넣어준다.

3. rows의 값들을 순차적으로 row에, cols의 값들을 순차적으로 col에 넣어 아래를 수행한다.
- $row + col$인 해당 위치의 값이 홀수인 경우, count를 증가시켜준다.

4. 반복이 완료되면 홀수의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CellsWithOddValuesInAMatrix.java){:target="_blank"}에서 확인 가능합니다.