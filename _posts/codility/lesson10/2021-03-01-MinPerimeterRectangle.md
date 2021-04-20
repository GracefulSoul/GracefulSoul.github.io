---
title: "Codility Java MinPerimeterRectangle"
excerpt: "Lesson10. Prime And Composite Numbers"
last_modified_at: 2021-03-01T15:18:00
header:
  image: /assets/images/codility/lesson10/MinPerimeterRectangle.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Prime And Composite Numbers
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/10-prime_and_composite_numbers/min_perimeter_rectangle/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int N) {
    int result = Integer.MAX_VALUE;
    for (int idx = 1; idx <= Math.sqrt(N); idx++) {
      if (N % idx == 0) {
        int temp = 2 * (idx + (N / idx));
        if (result > temp) {
          result = temp;
        }
      }
    }
    return result;
  }
}
```

# 설명
1. 최소 사각형의 둘레를 구하기 위해 결과 값을 저장하는 변수 result를 최대 정수형으로 저장한다.
2. 주어진 정수 N의 제곱근만큼 반복하여 사각형의 최소 둘레를 구한다.
  - 정수의 제곱근 이하의 정수 중에서 나머지가 0이 되는 숫자가 해당 정수 이하의 인수이다.
  - 정수를 정수 이하의 인수 중 하나로 나누면 해당 정수 이상의 인수가 된다.
  - 위에서 구한 두 인수의 합의 2배가 정수의 둘레가 된다.
3. 반복이 끝나면 최소 둘레를 저장하는 변수 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingQ26K5H-P53/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson10/MinPerimeterRectangle.java){:target="_blank"}에서 확인 가능합니다.