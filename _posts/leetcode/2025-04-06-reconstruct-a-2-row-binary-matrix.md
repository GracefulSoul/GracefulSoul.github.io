---
title: "Leetcode Java Reconstruct a 2-Row Binary Matrix"
excerpt: "Leetcode - 'Reconstruct a 2-Row Binary Matrix' 문제 Java 풀이"
last_modified_at: 2025-04-06T11:50:00
header:
  image: /assets/images/leetcode/reconstruct-a-2-row-binary-matrix.png
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
[Link](https://leetcode.com/problems/reconstruct-a-2-row-binary-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> reconstructMatrix(int upper, int lower, int[] colsum) {
    int sum = 0;
    for (int num : colsum) {
      sum += num;
    }
    if (sum != upper + lower) {
      return new ArrayList<>();
    } else {
      int length = colsum.length;
      int[][] result = new int[2][length];
      for (int i = 0; i < length; i++) {
        if (colsum[i] == 2 || (colsum[i] == 1 && lower < upper)) {
          result[0][i] = 1;
        }
        if (colsum[i] == 2 || (colsum[i] == 1 && result[0][i] == 0)) {
          result[1][i] = 1;
        }
        upper -= result[0][i];
        lower -= result[1][i];
      }
      return upper == 0 && lower == 0 ? new ArrayList(Arrays.asList(result[0], result[1])) : new ArrayList<>();
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/cells-with-odd-values-in-a-matrix/submissions/1598028767/){:target="_blank"}

# 설명
1. [0, 2] 범위의 값으로 구성된 colsum를 합이 upper인 List와 합이 lower인 List로 순차적으로 List로 감싸 반환하는 문제이다.
- 단, 구성이 불가능하면 빈 List를 주어진 문제의 결과로 반환한다.

2. colsum의 각 값의 합이 $upper + lower$와 동일하지 않는 조건을 만족할 수 없는 경우, 새 ArrayList를 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- length는 colsum의 길이를 저장한 변수이다.
- result는 결과를 만들 변수로, $2 \times length$ 크기의 2차원 정수 배열로 초기화한다.

4. 0부터 length까지 i를 증가시키며 아래를 반복한다.
- colsum[i]의 값이 2이거나 colsum[i]의 값이 1이면서 upper가 lower보다 클 경우, result[0][i]의 위치에 1을 넣어준다.
- colsum[i]의 값이 2이거나 colsum[i]의 값이 1이면서 result[0][i]의 값이 1인 upper에 넣지 않은 경우, result[1][i]의 위치에 1을 넣어준다.
- upper에 result[0][i]의 값을, lower에 result[1][i]의 값을 빼준다.

5. upper와 lower의 값이 0인지 여부에 따라 아래를 수행한다.
- 0인 두 List로 나눌 수 있는 경우, result[0]과 result[1]을 ArrayList로 변환 후 새 ArrayList에 넣어 주어진 문제의 결과로 반환한다.
- 0이 아닌 두 List로 나눌 수 없는 경우, 새 ArrayList를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReconstructA2RowBinaryMatrix.java){:target="_blank"}에서 확인 가능합니다.