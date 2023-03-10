---
title: "Leetcode Java Kth Smallest Element in a Sorted Matrix"
excerpt: "Leetcode Kth Smallest Element in a Sorted Matrix Java 풀이"
last_modified_at: 2022-02-07T18:00:00
header:
  image: /assets/images/leetcode/kth-smallest-element-in-a-sorted-matrix.png
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
[Link](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/){:target="_blank"}

# 코드
```java
class Solution {

  public int kthSmallest(int[][] matrix, int k) {
    int row = matrix.length;
    int col = matrix[0].length;
    int low = matrix[0][0];
    int high = matrix[row - 1][col - 1];
    while (low < high) {
      int mid = low + ((high - low) / 2);
      if (this.getCount(matrix, row, col, mid) < k) {
        low = mid + 1;
      } else {
        high = mid;
      }
    }
    return low;
  }

  private int getCount(int[][] matrix, int row, int col, int mid) {
    int count = 0;
    int j = col - 1;
    for (int i = 0; i < row; i++) {
      while (j >= 0 && matrix[i][j] > mid) {
        j--;
      }
      count += j + 1;
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/636319932/){:target="_blank"}

# 설명
1. 주어진 2차원 정수 배열인 matrix 내부 값들은 행 기준으로 오름차순 정렬되어 있으며, 해당 배열 내 값들 중 k번째로 작은 값을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row는 matrix의 행 개수를 저장할 변수로, matrix의 길이로 초기화한다.
- col는 matrix의 열 개수를 저장할 변수로, matrix의 첫 행의 길이로 초기화한다.
- low는 작은 값을 저장할 변수로, matrix의 가장 작은 값인 첫 위치의 정수를 넣어준다.
- high는 큰 값을 저장할 변수로, matrix의 가장 큰 값인 마지막 위치의 정수를 넣어준다.

3. low가 high보다 작을 때 까지 반복한다.
- mid의 $low + \frac{high - low}{2}$ 값을 넣어준다.
- 4번에서 정의한 getCount(int[][] matrix, int row, int col, int mid)를 수행한 결과에 따라 아래를 수행하고 반복을 계속 수행한다.
  - k보다 위의 값이 작은 경우 더 낮은 위치에 존재하므로, low에 $mid + 1$을 넣어 범위를 좁혀준다.
  - 그 외의 경우 더 높은 위치에 존재하므로, high에 mid를 넣어 범위를 좁혀준다.

4. 현재 위치에서 작은 값의 개수를 세기 위한 getCount(int[][] matrix, int row, int col, int mid) 메서드를 정의한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - count는 현재 값보다 작은 값의 개수를 저장할 변수로, 0으로 초기화한다.
  - j는 컬럼의 위치 값을 저장할 변수로, $col - 1$으로 초기화한다.
- 0부터 row까지 i를 증가시키며 반복을 수행한다.
  - j가 0보다 크거나 같고 matrix[i][j]의 값이 mid보다 큰 경우 해당 값 이전의 작은 값을 탐색하기 위해, j를 감소시키고 반복을 계속 수행한다.
  - 위의 반복이 완료되면 $j + 1$개의 작은 값들을 count에 넣어 준다.
- 반복이 완료되면 작은 값들의 개수인 count를 반환한다.

5. 3번의 반복이 완료되면 k번째로 작은 값인 low를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KthSmallestElementInASortedMatrix.java){:target="_blank"}에서 확인 가능합니다.