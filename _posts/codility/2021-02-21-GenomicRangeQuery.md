---
title: "Codility GenomicRangeQuery"
excerpt: "Lesson5. Prefix Sums"
last_modified_at: 2021-02-21T11:12:00
header:
  image: /assets/images/codility/GenomicRangeQuery.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Prefix Sums

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/5-prefix_sums/genomic_range_query/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
  public int[] solution(String S, int[] P, int[] Q) {
    int[] result = new int[P.length];
    // All array is start 0. (Check for changing character is exists.)
    int[] A = new int[S.length() + 1];
    int[] C = new int[S.length() + 1];
    int[] G = new int[S.length() + 1];
    // Initializing each array.
    for (int idx = 0; idx < S.length(); idx++) {
      A[idx + 1] = A[idx];
      C[idx + 1] = C[idx];
      G[idx + 1] = G[idx];
      switch(S.charAt(idx)) {
        case 'A': A[idx + 1]++; break;
        case 'C': C[idx + 1]++; break;
        case 'G': G[idx + 1]++; break;
        default: break;
      }
    }
    // Check for contains word in P and Q.
    for (int idx = 0; idx < P.length; idx++) {
      if (A[P[idx]] != A[Q[idx] + 1]) {
        result[idx] = 1;
      } else if (C[P[idx]] != C[Q[idx] + 1]) {
        result[idx] = 2;
      } else if (G[P[idx]] != G[Q[idx] + 1]) {
        result[idx] = 3;
      } else {
        result[idx] = 4;
      }
    }
    return result;
  }
}
```

# 설명
1. 주어진 DNA 문자열 S를 분석하기 위해 A, C, G 배열을 생성한다.
- DNA 문자열이 A, C, G에 해당하지 않으면 T로 간주한다.
2. A, C, G 배열은 각 index + 1 위치에 해당 문자열이 존재하면 문자열의 변화 감지를 위해 점층적으로 증가하도록 한다.
3. 주어진 배열 P와 Q의 값을 이용하여 최소 결과 값인 A부터 G 순으로 문자열의 변화를 분석한다.
- P[index] ~ Q[index]까지 A, C, G 배열에 변화가 존재한다면 DNA 영향 계수를 주어진 문제의 결과로 반환한다.
- 만일 위의 변화가 없으면 T로 간주하여 해당 DNA 영향 계수를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingQSWXB3-AAH/)

# 소스
[GitHub-GenomicRangeQuery](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson05/GenomicRangeQuery.java)