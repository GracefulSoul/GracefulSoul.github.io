---
title: "Leetcode Java Max Sum of Rectangle No Larger Than K"
excerpt: "Leetcode Max Sum of Rectangle No Larger Than K Java 풀이"
last_modified_at: 2022-01-28T13:00:00
header:
  image: /assets/images/leetcode/max-sum-of-rectangle-no-larger-than-k.png
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
[Link](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxSumSubmatrix(int[][] matrix, int k) {
    int row = matrix.length;
    int col = matrix[0].length;
    int max = Integer.MIN_VALUE;
    for (int i = 0; i < col; i++) {
      int[] nums = new int[row];
      for (int j = i; j < col; j++) {
        for (int l = 0; l < row; l++) {
          nums[l] += matrix[l][j];
        }
        max = Math.max(max, this.getMaxSubSum(nums, row, k));
        if (max == k) {
          return k;
        }
      }
    }
    return max;
  }

  private int getMaxSubSum(int[] nums, int row, int k) {
    int curr = nums[0];
    int max = curr;
    for (int idx = 1; idx < row; idx++) {
      curr = Math.max(curr + nums[idx], nums[idx]);
      if (curr > max) {
        max = curr;
      }
    }
    if (max <= k) {
      return max;
    }
    max = Integer.MIN_VALUE;
    for (int i = 0; i < row; i++) {
      curr = 0;
      for (int j = i; j < row; j++) {
        curr += nums[j];
        if (curr > max && curr <= k) {
          max = curr;
        }
        if (max == k) {
          return k;
        }
      }
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/629353823/){:target="_blank"}

# 설명
1. 주어진 2차원 배열 matrix를 이용하여 k보다 크지 않은 사각형 모양의 부분 영역 값들의 최대 합을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row는 matrix 행의 개수를 저장하는 변수로, matrix.length로 초기화 한다.
- col은 matrix 열의 개수를 저장하는 변수로, matrix[0].length로 초기화 한다.
- max는 k보다 크지 않은 부분 합을 저장할 변수로, 정수의 가장 작은 값으로 초기화 한다.

3. 0부터 col까지 i를 증가시키며 반복을 수행한다.
- nums는 각 부분 영역 값들의 합을 계산하기 위한 배열로, row 크기만큼의 배열로 정의한다.
  - i부터 col 미만까지 j를 증가시키며 nums를 초기화한다.
  - 0부터 row 미만까지 l을 증가시키며, nums의 l번째 값에 matrix[l][j]의 값을 더해준다.
  - max에 max와 4번에 정의한 getMaxSubSum(int[] nums, int row, int k)의 수행 결과 중 큰 값을 넣어준다.
  - max가 k와 동일한 경우 발생 가능한 최대의 크기이므로, k를 주어진 문제의 결과로 반환한다.
  - 위의 결과를 수행하여 순차적으로 반복을 계속 수행한다.
- 반복이 완료되면 k를 초과하지 않은 부분 영역 값들의 최대 합을 저장한 max를 주어진 문제의 결과로 반환한다.

4. 부분 영역 값들의 최대 값을 찾기 위한 getMaxSubSum(int[] nums, int row, int k) 메서드를 정의한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - curr은 현재 값을 임시 저장하기 위한 변수로, nums의 첫 값으로 초기화한다.
  - max는 최대 값을 저장하기 위한 변수로, curr의 값으로 초기화한다.
- 1부터 row 미만까지 반복하면서 최대 값을 max에 넣어준다.
  - curr에 $curr + nums[idx]$의 값과 nums[idx] 값 중 큰 값을 넣어준다.
  - curr이 max보다 큰 경우, max에 curr 값을 넣어준다.
- max가 k보다 작거나 같은 경우 해당 값이 가장 큰 값이므로, max를 반환한다.
- max에 정수의 가장 작은 값을 넣어 초기화 시켜준다.
- 0부터 row 미만까지 i를 증가시키며 반복을 수행한다.
  - curr을 0으로 초기화 한다.
  - i부터 row 미만까지 j를 증가시키며 max를 탐색한다.
  - curr에 nums[j] 값을 누적시킨다.
  - curr이 max보다 크고 k보다 같거나 작은 경우 가능한 최대 값이므로, max에 curr 값을 넣어준다.
  - max가 k와 동일한 경우 발생 가능한 최대의 크기이므로, k를 반환한다.
- 반복이 완료되면 nums에서 발생 가능한 최대 값인 max를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxSumOfRectangleNoLargerThanK.java){:target="_blank"}에서 확인 가능합니다.