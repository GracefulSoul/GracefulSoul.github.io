---
title: "Leetcode Java Trapping Rain Water II"
excerpt: "Leetcode Trapping Rain Water II Java 풀이"
last_modified_at: 2022-03-07T17:00:00
header:
  image: /assets/images/leetcode/trapping-rain-water-ii.png
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
[Link](https://leetcode.com/problems/trapping-rain-water-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int trapRainWater(int[][] heightMap) {
    int row = heightMap.length;
    int col = heightMap[0].length;
    int[][] volume = new int[row][col];
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        volume[i][j] = heightMap[i][j];
      }
    }
    boolean update = true;
    boolean init = true;
    while (update) {
      update = false;
      for (int i = 1; i < row - 1; i++) {
        for (int j = 1; j < col - 1; j++) {
          int val = Math.max(heightMap[i][j], Math.min(volume[i - 1][j], volume[i][j - 1]));
          if (init || val < volume[i][j]) {
            volume[i][j] = val;
            update = true;
          }
        }
      }
      init = false;
      for (int i = row - 2; i >= 1; i--) {
        for (int j = col - 2; j >= 1; j--) {
          int val = Math.max(heightMap[i][j], Math.min(volume[i + 1][j], volume[i][j + 1]));
          if (val < volume[i][j]) {
            volume[i][j] = val;
            update = true;
          }
        }
      }
    }
    int sum = 0;
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        if (volume[i][j] - heightMap[i][j] > 0) {
          sum += (volume[i][j] - heightMap[i][j]);
        }
      }
    }
    return sum;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/654958250/){:target="_blank"}

# 설명
1. 주어진 2차원 정수 배열 heightMap을 이용하여 빗물을 가둘 수 있는 물의 양을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row는 heightMap의 행의 개수를 저장하는 변수로, heightMap.length로 초기화한다.
- col은 heightMap의 열의 개수를 저장하는 변수로, heightMap[0].length로 초기화한다.
- volume은 주어진 heightMap의 빗물을 가둔 후 최대 높이를 저장할 배열로, heightMap의 값으로 초기화한다.
- update는 값의 수정 유무를 저장할 변수로, true로 초기화한다.
- init은 첫 수행 여부를 저장할 변수로, true로 초기화한다.

3. update가 true일 때 까지 반복하여 아래를 수행한다.
- update를 false로 수정하여 수정 내역이 없는 상태로 초기화한다.
- heightMap을 행과 열을 1부터 row와 col의 값보다 1 작게 반복하여 아래를 수행한다.
  - val에 volume[i - 1][j]의 값과 volume[i][j - 1]의 값 중 작은 값하고 heightMap[i][j]의 값 중 큰 값을 넣어준다.
  - 첫 수행이거나 val이 volume[i][j]보다 작아 물을 담을 높이보다 큰 경우, volume[i][j]에 val 값을 넣어 평준화 시키고 update를 true로 바꾸어 수정한 상태로 바꾸어준다.
- 첫 수행이 완료되었으므로, init을 false로 바꾸어준다.
- heightMap을 행과 열을 row와 col의 값보다 2 작은 값에서 1까지 반복하여 아래를 수행한다.
  - val에 volume[i + 1][j]의 값과 volume[i][j + 1]의 값 중 작은 값하고 heightMap[i][j]의 값 중 큰 값을 넣어준다.
  - val이 volume[i][j]의 값보다 작아 물을 담을 높이보다 큰 경우, volume[i][j]에 val 값을 넣어 평준화 시키고 update를 true로 바꾸어 수정한 상태로 바꾸어준다.

4. 반복이 완료되면 빗물을 가둘 수 있는 물의 양을 저장할 sum을 0으로 초기화시킨다.

5. volume을 반복하여 heightMap과 각 위치의 차이 값이 volume이 더 큰 경우, sum에 volume의 값과 heightMap의 값의 차이를 더해준다.

6. 위의 반복이 완료되면 빗물을 가둘 수 있는 물의 양을 저장한 sum을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TrappingRainWaterII.java){:target="_blank"}에서 확인 가능합니다.