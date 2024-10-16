---
title: "Leetcode Java Spiral Matrix II"
excerpt: "Leetcode Spiral Matrix II Java 풀이"
last_modified_at: 2021-06-08T18:00:00
header:
  image: /assets/images/leetcode/spiral-matrix-ii.png
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
[Link](https://leetcode.com/problems/spiral-matrix-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] generateMatrix(int n) {
    int[][] result = new int[n][n];
    int min = 0;
    int max = n - 1;
    int num = 1;
    while (num <= n * n) {
      for (int idx = min; idx <= max && num <= n * n; idx++) {
        result[min][idx] = num++;
      }
      for (int idx = min + 1; idx <= max - 1 && num <= n * n; idx++) {
        result[idx][max] = num++;
      }
      for (int idx = max; idx >= min && num <= n * n; idx--) {
        result[max][idx] = num++;
      }
      for (int idx = max - 1; idx >= min + 1 && num <= n * n; idx--) {
        result[idx][min] = num++;
      }
      min++;
      max--;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/504834978/){:target="_blank"}

# 설명
1. 기존 풀이한 [Spiral Matrix](../spiral-matrix/)와 비슷한 문제로, $n \times n$ 배열에 순차적으로 숫자를 넣는 문제이다.

2. 아래의 기본 변수들을 정의한다.
- 변수 result는 주어진 문제의 결과인 $n \times n$ 배열이다.
- 변수 min은 주어진 배열 matrix의 가로와 세로의 시작 인덱스이다.
- 변수 max는 주어진 배열 matrix의 가로와 세로의 최대 인덱스이다.
- 변수 num은 배열 내 채워질 값이다.

3. 반복문을 통해 순차적으로 배열 result의 외각부터 중심까지 변수 num을 증가시키며 num이 $n \times n$의 크기가 될 때까지 넣어준다.
- 우측 -> 아래 -> 좌측 -> 위 순으로 값들을 result에 넣는다.
- 외각 한바퀴를 돌면 min은 증가시키고, max는 증가시켜 반복문을 계속한다.

4. 반복이 종료되면 외각부터 숫자를 넣어 완성된 배열인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SpiralMatrixII.java){:target="_blank"}에서 확인 가능합니다.