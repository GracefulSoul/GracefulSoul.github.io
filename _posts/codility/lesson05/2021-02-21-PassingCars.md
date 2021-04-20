---
title: "Codility Java PassingCars"
excerpt: "Lesson5. Prefix Sums"
last_modified_at: 2021-02-21T11:44:00
header:
  image: /assets/images/codility/lesson05/PassingCars.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Prefix Sums
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/5-prefix_sums/passing_cars/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    int count = 0;
    int result = 0;
    for (int num : A) {
      if (num == 0) {
        count++;
      } else {
        result += count;
      }
      // If passing cars exeeds 1,000,000,000, return -1.
      if (result > 1000000000) {
        return -1;
      }
    }
    return result;
  }
}
```

# 설명
1. 동쪽으로 이동하는 차량 기준으로 차량의 숫자를 세면 된다. (기준을 서쪽으로 잡는 경우)
- 동쪽으로 이동하는 차량의 경우 count를 증가시킨다.
- 서쪽으로 이동하는 차량의 경우 동쪽으로 이동하는 차량의 수인 count를 결과인 result에 더해준다.
2. 만일 추월하는 차량의 수를 저장한 result가 1,000,000,000이 넘을 경우 -1을 주어진 문제의 결과로 반환한다.
3. 반복이 완료되면 추월된 차량의 수를 저장한 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingSVXSS6-HYF/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson05/PassingCars.java){:target="_blank"}에서 확인 가능합니다.