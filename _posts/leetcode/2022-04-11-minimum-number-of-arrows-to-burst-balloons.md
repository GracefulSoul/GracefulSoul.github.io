---
title: "Leetcode Java Minimum Number of Arrows to Burst Balloons"
excerpt: "Leetcode Minimum Number of Arrows to Burst Balloons Java 풀이"
last_modified_at: 2022-04-11T12:00:00
header:
  image: /assets/images/leetcode/minimum-number-of-arrows-to-burst-balloons.png
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
[Link](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/){:target="_blank"}

# 코드
```java
class Solution {

  public int findMinArrowShots(int[][] points) {
    Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));
    int point = points[0][1];
    int count = 1;
    for (int idx = 1; idx < points.length; idx++) {
      if (points[idx][0] > point) {
        point = points[idx][1];
        count++;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/677982219/){:target="_blank"}

# 설명
1. 풍선의 x축 너비를 나타내는 points 내 풍선들을 y축으로 수직 발사하는 화살로 터트릴 경우 필요한 화살의 갯수를 구하는 문제이다.
- point[i] = [x<sub>start</sub>, x<sub>end</sub>]

2. points를 풍선 너비의 끝(우측) 지점을 기준으로 오름차순 정렬을 수행한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- point는 이전 풍선의 너비 중 마지막 값을 저장하기 위한 변수로, 정렬된 points 내 첫 풍선의 끝 지점의 값을 넣어준다.
- count는 화살의 갯수를 구하기 위한 변수로, 첫 풍선을 터트리기 위한 1개로 초기화한다.

4. 1부터 points의 길이 전까지 idx를 증가시키며 아래를 반복한다.
- points의 idx번째 풍선의 시작(좌측) 지점이 point보다 큰 경우 기존 화살로 같이 터트릴 수 없으므로, point에 해당 풍선의 끝(우측) 지점의 값을 넣어주고 count를 증가시킨다.

5. 반복이 완료되면 화살의 갯수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfArrowsToBurstBalloons.java){:target="_blank"}에서 확인 가능합니다.