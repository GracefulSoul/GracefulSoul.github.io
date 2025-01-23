---
title: "Leetcode Java Count Servers that Communicate"
excerpt: "Leetcode - 'Count Servers that Communicate' 문제 Java 풀이"
last_modified_at: 2025-01-23T09:10:00
header:
  image: /assets/images/leetcode/count-servers-that-communicate.png
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
[Link](https://leetcode.com/problems/count-servers-that-communicate/){:target="_blank"}

# 코드
```java
class Solution {

  public int countServers(int[][] grid) {
    int rowLength = grid.length;
    int colLength = grid[0].length;
    int[] rowCounts = new int[rowLength];
    int[] colCounts = new int[colLength];
    for (int i = 0; i < rowLength; i++) {
      for (int j = 0; j < colLength; j++) {
        if (grid[i][j] == 1) {
          rowCounts[i]++;
          colCounts[j]++;
        }
      }
    }
    int result = 0;
    for (int i = 0; i < rowLength; i++) {
      for (int j = 0; j < colLength; j++) {
        if (grid[i][j] == 1 && (rowCounts[i] > 1 || colCounts[j] > 1)) {
          result++;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-servers-that-communicate/submissions/1517403089/){:target="_blank"}

# 설명
1. 컴퓨터의 위치가 저장된 grid를 이용하여 동일한 열과 행의 컴퓨터끼리 통신이 가능한 컴퓨터의 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- rowLength와 colLength는 grid의 행과 열의 길이를 저장한 변수이다.
- rowCounts와 colCounts는 grid의 행과 열에 존재하는 컴퓨터 갯수를 계산하기 위한 변수로, 행과 열의 크기에 해당하는 정수 배열로 초기화하고 grid를 반복하여 행과 열에 존재하는 컴퓨터의 갯수를 계산한다.
- result는 통신 가능한 컴퓨터의 수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 rowLength 미만까지 i를 증가시키고, 0부터 colLength 미만까지 j를 증가시키며 아래를 반복한다.
- gird[i][j]의 값이 1인 컴퓨터가 존재하면서 rowCounts[i] 혹은 colCounts[j]가 1보다 큰 통신 가능한 컴퓨터가 존재하는 경우, result를 증가시켜 통신 가능한 컴퓨터의 수를 계산한다.

4. 반복이 완료되어 계산된 통신 가능한 컴퓨터의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountServersThatCommunicate.java){:target="_blank"}에서 확인 가능합니다.