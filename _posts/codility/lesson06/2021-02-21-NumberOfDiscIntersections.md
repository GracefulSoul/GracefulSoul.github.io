---
title: "Codility Java NumberOfDiscIntersections"
excerpt: "Lesson6. Sorting"
last_modified_at: 2021-02-21T12:46:00
header:
  image: /assets/images/codility/lesson06/NumberOfDiscIntersections.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Sorting
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/6-sorting/number_of_disc_intersections/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int[] A) {
    int result = 0;
    long[] left = new long[A.length];
    long[] right = new long[A.length];
    // Save left and right point each array.
    for (int idx = 0; idx < A.length; idx++) {
      left[idx] = idx - (long) A[idx];
      right[idx] = idx + (long) A[idx];
    }
    Arrays.sort(left);
    Arrays.sort(right);
    int num = 0;
    // Calculate intersects with left and right point.
    for (int idx = 0; idx < A.length; idx++) {
      while (num < A.length && right[idx] >= left[num]) {
        result += num - idx;
        num++;
      }
    }
    // If the number of intersecting pairs excceds 10,000,000.
    if (result > 10000000) {
      return -1;
    }
    return result;
  }
}
```

# 설명
1. 주어진 배열 A를 이용하여 x축과 디스크의 접점을 배열 left, right에 담는다.
2. 배열 left와 right를 Arrays 클래스를 활용하여 오름차순 정렬한다.
3. 배열 left와 right를 아래의 내용을 참고하여 디스크들의 접점이 존재하는지를 계산한다.
    1. 한 디스크의 우측 x축 접점 기준으로 다른 디스크의 좌측 x축 접점 위치가 작은 경우 두 디스크의 접점이 존재하지 않는다. 
    2. 한 디스크의 우측 x축 접점 기준으로 다른 디스크의 좌측 x축 접점이 동일한 경우 두 디스크의 접점이 한 개이다. (result + 1)
    3. 한 디스크의 우측 x축 접점 기준으로 다른 디스크의 좌측 x축 접점 위치가 큰 경우 두 디스크의 접점이 두 개이다. (result + 1)
4. 디스크들의 교차 수를 저장한 result가 10,000,000보다 큰 경우, -1을 주어진 문제의 결과로 반환한다.
5. 디스크들의 교차 수를 저장한 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingY8JCA7-Z55/)

# 소스
[GitHub-NumberOfDiscIntersections](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson06/NumberOfDiscIntersections.java)