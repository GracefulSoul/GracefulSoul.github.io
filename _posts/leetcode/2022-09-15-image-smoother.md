---
title: "Leetcode Java Image Smoother"
excerpt: "Leetcode Image Smoother Java"
last_modified_at: 2022-09-15T19:40:00
header:
  image: /assets/images/leetcode/image-smoother.png
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
[Link](https://leetcode.com/problems/image-smoother){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] imageSmoother(int[][] img) {
    int row = img.length;
    int col = img[0].length;
    int[][] result = new int[row][col];
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < col; j++) {
        result[i][j] = this.caculate(img, row, col, i, j);
      }
    }
    return result;
  }

  private int caculate(int[][] img, int row, int col, int i, int j) {
    int count = 1;
    int sum = img[i][j];
    if (i - 1 >= 0) {
      count++;
      sum += img[i - 1][j];
      if (j - 1 >= 0) {
        count++;
        sum += img[i - 1][j - 1];
      }
      if (j + 1 < col) {
        count++;
        sum += img[i - 1][j + 1];
      }
    }
    if (j - 1 >= 0) {
      count++;
      sum += img[i][j - 1];
    }
    if (j + 1 < col) {
      count++;
      sum += img[i][j + 1];
    }
    if (i + 1 < row) {
      count++;
      sum += img[i + 1][j];
      if (j - 1 >= 0) {
        count++;
        sum += img[i + 1][j - 1];
      }
      if (j + 1 < col) {
        count++;
        sum += img[i + 1][j + 1];
      }
    }
    return sum / count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/800377895/){:target="_blank"}

# 설명
1. img 배열 의 각 요소 별 자신을 포함한 인접한 셀 값들의 평균 값을 넣은 배열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 img의 행과 열의 개수를 넣어 보관할 변수이다.
- result는 img를 이용하여 결과를 넣을 배열로, img와 동일한 크기로 초기화한다.

3. img의 모든 값들을 이용하여 모든 셀들의 값들에 4번에서 정의한 caculate(int[][] img, int row, int col, int i, int j) 메서드를 수행한 결과를 넣어준다.

4. 자신을 포함한 인접한 셀들의 값의 평균을 계산하기위한 caculate(int[][] img, int row, int col, int i, int j) 메서드를 정의한다.
- 인접한 셀의 개수인 count를 1로, 자신을 포함한 인접한 셀들의 합을 저장할 sum을 현재 셀의 값인 img[i][j]으로 초기화한다.
- 해당 위치의 위, 아래, 왼쪽, 오른쪽과 대각선에 위치한 셀의 유무를 확인하여 count를 증가시키고 sum에 각 값을 더해준다.
- 소수점을 절사한 정수를 반환해야 하므로 $\frac{sum}{count}$의 정수 값만 반환한다.

5. 반복이 완료되면 결과를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ImageSmoother.java){:target="_blank"}에서 확인 가능합니다.