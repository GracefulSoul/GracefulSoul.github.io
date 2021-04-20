---
title: "Codility Java MinMaxDivision"
excerpt: "Lesson14. Binary Search Algorithm"
last_modified_at: 2021-03-13T12:03:00
header:
  image: /assets/images/codility/lesson14/MinMaxDivision.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Binary Search Algorithm
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/14-binary_search_algorithm/min_max_division/){:target="_blank"}

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int solution(int K, int M, int[] A) {
    int sum = 0;
    int max = 0;
    for (int idx = 0; idx < A.length; idx++) {
      sum += A[idx];
      if (A[idx] > max) {
        max = A[idx];
      }
    }
    int result = sum;
    while (max <= sum) {
      int mid = (max + sum) / 2;
      if (isDivisable(mid, K, A)) {
        result = mid;
        sum = mid - 1;
      } else {
        max = mid + 1;
      }
    }
    return result;
  }
  private boolean isDivisable(int mid, int K, int[] A) {
    int size = K;
    int sum = 0;
    for (int idx = 0; idx < A.length; idx++) {
      sum = sum + A[idx];
      if (sum > mid) {
        size--;
        sum = A[idx];
      }
      if (size == 0) {
        return false;
      }
    }
    return true;
  }
}

```

# 설명
1. 주어진 배열 A의 합계와 배열 내 최대 값을 확인한다.
2. 블록을 나누어 한 블록의 최대 합계가 다른 경우보다 최소가 되는 수를 구하기 위해 이진 검색을 활용하여 탐색한다.
  - 이진 검색은 주어진 배열 A의 합계를 초기 값으로 저장한(이하 상한) 정수 sum보다 주어진 배열 A내 최대 값을 저장한 정수 max(이하 하한)가 작거나 같을 경우 계속 수행한다.
  - 한 블록에 모든 값이 포함된 경우가 최대값이기 때문에 초기 결과 값으로 지정한다.
  - 상한 값과 하한 값을 2로 나누어 변수 mid를 선언하고, 이진 검색을 수행한다.
    - 이진 검색에 활용하는 mid 변수를 이용하여 주어진 배열 A를 K 블록으로 분할 가능한지 확인한다.
  - 만일 K 블록으로 분할이 불가능하면(반복 도중 size가 0이 될 경우) 하한을 mid + 1 값으로 변경하여 이진 검색을 계속 수행한다.
  - 만일 K 블록으로 분할이 가능하면 결과 값을 저장하는 result 변수에 mid 값을 넣고, 상한을 mid - 1 값으로 변경하여 이진 검색을 계속 수행한다.
3. 반복이 종료되면 결과 값을 저장한 변수 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingTRFHH9-GJE/){:target="_blank"}

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/codility/blob/master/src/main/java/gracefulsoul/lesson14/MinMaxDivision.java){:target="_blank"}에서 확인 가능합니다.
