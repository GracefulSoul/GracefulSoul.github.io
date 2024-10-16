---
title: "Leetcode Java Max Increase to Keep City Skyline"
excerpt: "Leetcode Max Increase to Keep City Skyline Java"
last_modified_at: 2023-01-16T19:20:00
header:
  image: /assets/images/leetcode/max-increase-to-keep-city-skyline.png
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
[Link](https://leetcode.com/problems/max-increase-to-keep-city-skyline){:target="_blank"}

# 코드
```java
class Solution {

  public int maxIncreaseKeepingSkyline(int[][] grid) {
    int length = grid.length;
    int[] row = new int[length];
    int[] col = new int[length];
    for (int i = 0; i < length; i++) {
      for (int j = 0; j < length; j++) {
        row[i] = Math.max(row[i], grid[i][j]);
        col[j] = Math.max(col[j], grid[i][j]);
      }
    }
    int result = 0;
    for (int i = 0; i < length; i++) {
      for (int j = 0; j < length; j++) {
        result += Math.min(row[i], col[j]) - grid[i][j];
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/max-increase-to-keep-city-skyline/submissions/879135989/){:target="_blank"}

# 설명
1. 각 건물의 높이가 저장된 grid를 이용하여 네 방향에서 보았을 때 동일한 외부 윤곽을 유지하면서 올릴 수 있는 최대한의 건물 높이로 건물을 증축할 때, 증축할 수 있는 건물들의 높이 합을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 grid 행의 길이를 저장한 변수이다.
- row는 각 행별 가장 큰 높이를 저장하기 위한 배열로, length 길이로 초기화한다.
- col은 각 열별 가장 큰 높이를 저장하기 위한 배열로, length 길이로 초기화한다.

3. 0부터 length까지 i와 j를 증가시키며 row와 col에 각 행과 열의 가장 큰 값을 저장한다.

4. result는 올릴 수 있는 높이를 저장할 변수로, 0으로 초기화한다.

5. 0부터 length까지 i와 j를 증가시키며 아래를 수행한다.
- result에 row의 i번째 값과 col의 j번째 값중 가장 낮은 높이에 grid[i][j]의 값을 뺀 증가할 수 있는 높이를 더해준다.

6. 반복이 완료되면 각 건물의 증축 횟수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxIncreaseToKeepCitySkyline.java){:target="_blank"}에서 확인 가능합니다.