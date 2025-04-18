---
title: "Codility Java BinaryGap"
excerpt: "Lesson1. Iterations"
last_modified_at: 2021-02-20T13:49:00
header:
  image: /assets/images/codility/lesson01/BinaryGap.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Iterations
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/1-iterations/binary_gap/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int N) {
    char[] binary = Integer.toBinaryString(N).toCharArray();
    int max = 0;
    int counter = 0;
    // Loop and check max length.
    for (int idx = 1; idx < binary.length; idx++) {
      if(binary[idx] == '0') {
        counter++;
      } else {
        if (counter > max) {
          max = counter;
        }
        // Initializing counter.
        counter = 0;
      }
    }
    return max;
  }
}
```

# 결과
[Link](https://app.codility.com/demo/results/trainingE5EF2K-44N/){:target="_blank"}

# 설명
1. 주어진 숫자를 Binary로 변환한다.
2. Binary를 순차 확인하며, 1사이의 0의 개수를 센다.
- Binary의 시작은 항상 1부터로, Index 1부터 탐색한다.
- 1이 나타날 경우 max에 임시 저장하고, counter를 초기화하여 다시 개수를 센다.
3. 문제의 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson01/BinaryGap.java){:target="_blank"}에서 확인 가능합니다.