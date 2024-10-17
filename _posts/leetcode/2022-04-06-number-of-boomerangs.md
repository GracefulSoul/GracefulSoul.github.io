---
title: "Leetcode Java Number of Boomerangs"
excerpt: "Leetcode - 'Number of Boomerangs' 문제 Java 풀이"
last_modified_at: 2022-04-06T12:00:00
header:
  image: /assets/images/leetcode/number-of-boomerangs.png
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
[Link](https://leetcode.com/problems/number-of-boomerangs/){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfBoomerangs(int[][] points) {
    int number = 0;
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < points.length; i++) {
      for (int j = 0; j < points.length; j++) {
        if (i == j) {
          continue;
        }
        int distance = this.calculateDistance(points[i], points[j]);
        int point = map.getOrDefault(distance, 0);
        if (point > 0) {
          number += point * 2;
        }
        map.put(distance, point + 1);
      }
      map.clear();
    }
    return number;
  }

  private int calculateDistance(int[] pointA, int[] pointB) {
    int x = pointB[0] - pointA[0];
    int y = pointB[1] - pointA[1];
    return (x * x) + (y * y);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/674759531/){:target="_blank"}

# 설명
1. 평면 위에 존재하는 points를 이용하여 point(i, j, k)에서 i와 j 사이의 거리가 i와 k 사이의 거리와 동일하게 지나가는 부메랑의 수를 구하는 문제이다.
- points 내 i번째 존재하는 점인 point[i]는 [x<sub>i</sub>, y<sub>i</sub>]로 표현한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- number는 각 점을 지나는 부메랑의 개수를 세기 위한 변수로, 0으로 초기화한다.
- map은 동일한 거리의 점의 수를 저장할 변수로, HashMap으로 초기화한다.

3. 0부터 point의 길이 전까지 i를 증가시키며 아래의 반복을 수행한다.
- 0부터 point의 길이 전까지 j를 증가시키며 아래의 반복을 다시 수행한다.
  - i와 j가 동일한 경우, 다음 반복을 계속 수행한다.
  - distance에 4번에서 정의한 calculateDistance(int[] pointA, int[] pointB) 메서드를 수행하여 a와 b 사이의 거리를 넣어준다.
  - map에서 distance가 같은 점이 존재하는지 여부를 확인하여 point에 넣고, 없으면 0을 넣어준다.
  - point가 1개 이상인 경우, 부메랑은 곡선으로 순하여 다시 돌아오므로, 돌아오는 쪽에서 던져서 던지는 쪽에서 받는 경우를 포함하여 number에 point의 2배를 넣어준다.
  - map에 dsitance에 해당하는 값에 $point + 1$로 넣어준다.
- map을 초기화 시켜주고 반복을 계속 수행한다.

4. 두 점 사이의 거리를 계산하기 위한 calculateDistance(int[] pointA, int[] pointB) 메서드를 정의한다.
- pointA와 pointB 사이의 x축 거리를 변수 x에 넣고, y에 축 거리를 변수 y에 넣어준다.
- 거리를 구하기 위한 기본 공식에서 제곱근을 수행하기 전인 x의 제곱과 y의 제곱의 합을 반환한다.
  - $x = y$이면 $x^2 = y^2$이고, $\sqrt{x} = \sqrt{y}$가 성립하므로 제곱근을 수행하지 않은 값이 동일하지 않은 경우, 거리 또한 동일하지 않는다.

5. 반복이 완료되면 부메랑의 수인 number를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfBoomerangs.java){:target="_blank"}에서 확인 가능합니다.