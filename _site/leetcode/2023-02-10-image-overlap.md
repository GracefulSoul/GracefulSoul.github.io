---
title: "Leetcode Java Image Overlap"
excerpt: "Leetcode Image Overlap Java"
last_modified_at: 2023-02-10T21:11:00
header:
  image: /assets/images/leetcode/image-overlap.png
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
[Link](https://leetcode.com/problems/image-overlap){:target="_blank"}

# 코드
```java
class Solution {

  public int largestOverlap(int[][] img1, int[][] img2) {
    int length = img1.length;
    int[][] count = new int[(2 * length) + 1][(2 * length) + 1];
    for (int x1 = 0; x1 < length; x1++) {
      for (int y1 = 0; y1 < length; y1++) {
        if (img1[x1][y1] == 1) {
          for (int x2 = 0; x2 < length; x2++) {
            for (int y2 = 0; y2 < length; y2++) {
              if (img2[x2][y2] == 1) {
                count[x1 - x2 + length][y1 - y2 + length]++;
              }
            }
          }
        }
      }
    }
    int result = 0;
    for (int[] row : count) {
      for (int value : row) {
        result = Math.max(result, value);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/image-overlap/submissions/895306409/){:target="_blank"}

# 설명
1. $n \times n$의 2차원 배열인 img1을 상하좌우 한 칸씩 이동하여 img2와 겹치는 칸의 개수가 가장 큰 값을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 img1의 길이를 저장한 변수이다.
- count는 img1과 img2를 이용하여 중첩된 칸의 개수를 계산하기 위한 변수로, $length \times 2$보다 1 큰 크기의 2차원 배열로 초기화한다.

3. 0부터 length 미만까지 x1과 y1을 증가시키며 img1[x1][y1]의 값이 1이면 아래를 수행한다.
- 0부터 length 미만까지 x2와 y2를 증가시키며 img2[x2][y2]의 값이 1이면 img1과 img2가 겹치는 구간이므로 아래를 수행한다.
  - count의 [$x1 - x2 + length$][$y1 - y2 + length]번째 값을 증가시켜 겹치는 구간을 개수를 증가시킨다.

4. result는 최대 개수를 저장하기 위한 변수로, count의 모든 값들을 확인하여 최댓 값을 넣고 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ImageOverlap.java){:target="_blank"}에서 확인 가능합니다.