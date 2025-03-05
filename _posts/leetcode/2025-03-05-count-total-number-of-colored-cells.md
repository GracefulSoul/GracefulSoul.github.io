---
title: "Leetcode Java Count Total Number of Colored Cells"
excerpt: "Leetcode - 'Count Total Number of Colored Cells' 문제 Java 풀이"
last_modified_at: 2025-03-05T18:20:00
header:
  image: /assets/images/leetcode/count-total-number-of-colored-cells.png
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
[Link](https://leetcode.com/problems/count-total-number-of-colored-cells/){:target="_blank"}

# 코드
```java
class Solution {

  public long coloredCells(int n) {
    return 1 + (4L * (n * (n - 1) / 2));
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-total-number-of-colored-cells/submissions/1563548976/){:target="_blank"}

# 설명
1. 1분에 가운데 하나의 정사각형으로 시작하여, 시간의 흐름에 따라 마름모 모양으로 사각형이 상하좌우 및 대각선 방향으로 증식한다. n 분 이후 해당 사각형의 갯수를 계산하는 문제이다.

2. 처음 하나부터 시작하여 네 방면으로 4의 배수만큼 증식하므로, $1 + 4 \times \frac{n \times (n - 1)}{2}$의 값을 주어진 문제의 결과로 반환한다.
- $n \times (n - 1)$ 값이 매우 클 수 있으므로, 4를 long타입으로 적용하여 같이 계산해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountTotalNumberOfColoredCells.java){:target="_blank"}에서 확인 가능합니다.