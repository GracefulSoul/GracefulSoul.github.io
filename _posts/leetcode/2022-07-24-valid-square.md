---
title: "Leetcode Java Valid Square"
excerpt: "Leetcode Valid Square Java"
last_modified_at: 2022-07-24T13:30:00
header:
  image: /assets/images/leetcode/nvalid-square.png
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
[Link](https://leetcode.com/problems/valid-square/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean validSquare(int[] p1, int[] p2, int[] p3, int[] p4) {
    long a = this.getDistance(p1, p2);
    long b = this.getDistance(p1, p3);
    long c = this.getDistance(p1, p4);
    if (a != this.getDistance(p3, p4) || b != this.getDistance(p2, p4) || c != this.getDistance(p2, p3) ||
        a == 0 || b == 0 || c == 0) {
      return false;
    } else {
      return a == b || b == c || a == c;
    }
  }
    
    private long getDistance(int[] p1, int[] p2) {
        return (p1[0] - p2[0]) * (p1[0] - p2[0]) + (p1[1] - p2[1]) * (p1[1] - p2[1]);
    }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/755102078/){:target="_blank"}

# 설명
1. 네 점인 p1, p2, p3, p4를 연결하면 사각형이 되는지 검증하는 문제이다.

2. 두 점 사이의 거리를 계산할 getDistacne(int[] p1, int[] p2) 메서드를 정의한다.
- 두 점의 길이는 $\sqrt{(x1 - x2)^2 + (y1 - y2)^2}$ 이지만, 거리를 구하는 문제가 아니므로 제곱근을 사용하지 않은 값으로도 검증이 가능하여 공식의 결과를 반환한다.

3. a, b, c에 p1과 p2, p1과 p3, p1과 p4의 거리를 순차적으로 넣어준다.

4. 아래의 경우를 만족하면 false를 주어진 문제의 결과로 반환한다.
- p1과 p2 간의 거리인 a가 p3과 p4 간의 거리가 같지 않은 경우, 다른 두 선이 동일한 길이가 되지 않으므로 사각형이 될 수 없다.
- p1과 p3 간의 거리인 b가 p2와 p4 간의 거리가 같지 않은 경우도 위와 동일한 이유로 사각형이 될 수 없다.
- p1과 p4 간의 거리인 c가 p2와 p3 간의 거리가 같지 않은 경우도 위와 동일한 이유로 사각형이 될 수 없다.
- a혹은 b, c가 0인 경우 사각형을 이루는 한 변의 길이가 0이므로, 사각형이 될 수 없다.

5. 그 외의 경우, a와 b가 같거나, b와 c가 같거나 a와 c가 같은지 여부를 주어진 문제의 결과로 반환한다.
- p1 기준으로 각 점 간의 길이를 저장한 a, b, c 중 두 선의 길이가 같으면 사각형을 구성하는 기본 조건을 만족하므로 true를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidSquare.java){:target="_blank"}에서 확인 가능합니다.