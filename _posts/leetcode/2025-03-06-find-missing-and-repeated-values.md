---
title: "Leetcode Java Count Total Number of Colored Cells"
excerpt: "Leetcode - 'Count Total Number of Colored Cells' 문제 Java 풀이"
last_modified_at: 2025-03-06T17:40:00
header:
  image: /assets/images/leetcode/find-missing-and-repeated-values.png
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
[Link](https://leetcode.com/problems/find-missing-and-repeated-values/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] findMissingAndRepeatedValues(int[][] grid) {
    int length = grid.length;
    int[] result = new int[2];
    int[] counts = new int[(length * length) + 1];
    for (int[] row : grid) {
      for (int value : row) {
        if (counts[value] == 1) {
          result[0] = value;
        } else {
          counts[value]++;
        }
      }
    }
    for (int i = 1; i < counts.length; i++) {
      if (counts[i] == 0) {
        result[1] = i;
        break;
      }
    }
    if (result[1] == 0) {
      result[1] = counts.length;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-missing-and-repeated-values/submissions/1564678616/){:target="_blank"}

# 설명
1. 2차원 정사각형 크기의 배열 grid 내 두 번 존재하는 값과 누락된 값을 찾아 배열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 grid의 길이를 저장한 변수이다.
- result는 결과를 저장할 변수로, 두 값을 반환하기 위해 2 크기의 정수 배열로 초기화한다.
- counts는 grid 내 값의 갯수를 계산하기 위한 변수로, 1-index 기준으로 값의 상한 값까지 들어가기 위해 $(length \times length) + 1$ 크기의 정수 배열로 초기화하한다.

3. grid 내 첫 행부터 마지막 행까지 첫 열부터 마지막 열까지 순차적으로 값들을 탐색하면 중복된 값이 존재하는 경우, result[0]에 해당 값을 넣어주면서 counts 배열 내 값의 갯수를 계산한다.

4. 1부터 counts 길이 미만까지 i를 증가시키며, count[i]의 값이 0인 값을 찾아 result[1]에 넣어주고 반복을 중지시킨다.

5. result[1]의 값이 0인 누락된 값이 존재하지 않는 경우, result[1]에 counts.length인 다음 가능한 값을 넣어준다.

6. 모든 수행이 완료되어 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindMissingAndRepeatedValues.java){:target="_blank"}에서 확인 가능합니다.