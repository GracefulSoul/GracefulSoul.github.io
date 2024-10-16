---
title: "Leetcode Java Valid Boomerang"
excerpt: "Leetcode Valid Boomerang Java"
last_modified_at: 2024-02-06T21:20:00
header:
  image: /assets/images/leetcode/valid-boomerang.png
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
[Link](https://leetcode.com/problems/valid-boomerang){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isBoomerang(int[][] points) {
    return (points[0][0] - points[1][0]) * (points[0][1] - points[2][1]) !=
        (points[0][0] - points[2][0]) * (points[0][1] - points[1][1]);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/valid-boomerang/submissions/1167759099/){:target="_blank"}

# 설명
1. 세 점의 위치가 있는 points가 부메랑 같이 휘어있는지 구하는 문제이다.

2. 세 점의 위치가 휘어 있다는 것은 한 점에서 나머지 두 점까지의 기울기가 다르다는 의미이므로, 기울기를 구하는 공식을 대입하여 계산한다.
- $\frac{points[0][0] - points[1][0]}{points[0][1] - points[1][1]} != \frac{points[0][0] - points[2][0]}{points[0][1] - points[2][1]}$ 를 성립한다.
- 위의 경우, 분모가 0이 되는 경우는 성립이 되지 않으므로 분모에 해당하는 공식을 양 변에 각각 곱해준다.
- $(points[0][0] - points[1][0]) \times (points[0][1] - points[2][1]) != (points[0][0] - points[2][0]) \times (points[0][1] - points[1][1])$ 이 성립한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidBoomerang.java){:target="_blank"}에서 확인 가능합니다.