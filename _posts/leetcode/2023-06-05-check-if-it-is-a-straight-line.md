---
title: "Leetcode Java Check If It Is a Straight Line"
excerpt: "Leetcode Easy - 'Check If It Is a Straight Line' 문제 Java 풀이"
last_modified_at: 2023-06-05T18:50:00
header:
  image: /assets/images/leetcode/check-if-it-is-a-straight-line.png
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
[Link](https://leetcode.com/problems/check-if-it-is-a-straight-line){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkStraightLine(int[][] coordinates) {
    int x = coordinates[1][0];
    int y = coordinates[1][1];
    int dx = x - coordinates[0][0];
    int dy = y - coordinates[0][1];
    for (int[] coordinate : coordinates) {
      if (dx * (coordinate[1] - y) != dy * (coordinate[0] - x)) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-it-is-a-straight-line/submissions/964275575/){:target="_blank"}

# 설명
1. 점의 위치를 넣은 coordinates가 직선으로 위치하는지를 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- x와 y에 coordinates의 두 번째 값의 좌표를 순서대로 넣어준다.
- dx와 dy에 x와 coordinates의 첫 뻔째 값의 좌표의 차잇값을 넣어준다.

3. coordinates의 모든 값을 이용하여 아래를 반복한다.
- dx와 coordinate의 두 번째 값에 y를 뺀 값을 곱한 결과와 dy에 coordinate의 첫 번째 값에 x를 뺀 값을 곱한 결과가 같지 않으면 기울기가 달라졌으므로 false를 반환한다.

4. 반복이 완료되면 일자로 이어져 있으므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfItIsAStraightLine.java){:target="_blank"}에서 확인 가능합니다.