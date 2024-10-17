---
title: "Leetcode Java Equal Row and Column Pairs"
excerpt: "Leetcode Medium - 'Equal Row and Column Pairs' 문제 Java 풀이"
last_modified_at: 2023-06-13T19:00:00
header:
  image: /assets/images/leetcode/equal-row-and-column-pairs.png
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
[Link](https://leetcode.com/problems/equal-row-and-column-pairs){:target="_blank"}

# 코드
```java
class Solution {

  public int equalPairs(int[][] grid) {
    int result = 0;
    int length = grid.length;
    for (int i = 0; i < length; i++) {
      for (int j = 0; j < length; j++) {
        int k = 0;
        while (k < length) {
          if (grid[i][k] != grid[k][j]) {
            break;
          }
          k++;
        }
        result += k == length ? 1 : 0;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/equal-row-and-column-pairs/submissions/970263675/){:target="_blank"}

# 설명
1. $n \times n$ 크기의 grid 내 [r<sub>i</sub>, c<sub>i</sub>] 지점에서 행과 열의 시작부터 끝까지 값의 조합이 동일하게 되는 위치의 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 행과 열의 시작부터 끝까지 값의 조합이 동일하게 되는 위치의 갯수를 계산할 변수로, 0으로 초기화한다.
- length는 grid의 길이를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키고, 0부터 length 미만까지 j를 증가시키며 아래를 반복한다.
- k에 0을 넣고, k가 length 미만까지 아래를 반복한다.
  - grid[i][k]의 값이 grid[k][j]의 값과 다른 경우, 행과 열의 동일한 순번의 값이 다르게 되므로 반복을 멈춘다.
  - k를 증가시키고 다음 자리를 검증한다.
- k와 length가 동일한 위의 경우를 만족하는 위치인 경우에 result에 1을 더해준다.

4. 반복이 모두 완료되면 위치의 갯수가 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EqualRowAndColumnPairs.java){:target="_blank"}에서 확인 가능합니다.