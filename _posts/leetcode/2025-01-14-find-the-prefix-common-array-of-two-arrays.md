---
title: "Leetcode Java Find the Prefix Common Array of Two Arrays"
excerpt: "Leetcode - 'Find the Prefix Common Array of Two Arrays' 문제 Java 풀이"
last_modified_at: 2025-01-14T19:10:00
header:
  image: /assets/images/leetcode/find-the-prefix-common-array-of-two-arrays.png
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
[Link](https://leetcode.com/problems/find-the-prefix-common-array-of-two-arrays/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] findThePrefixCommonArray(int[] A, int[] B) {
    int length = A.length;
    int[] counts = new int[length + 1];
    int[] result = new int[length];
    int common = 0;
    for (int i = 0; i < length; i++) {
      if (++counts[A[i]] == 2) {
        common++;
      }
      if (++counts[B[i]] == 2) {
        common++;
      }
      result[i] = common;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-prefix-common-array-of-two-arrays/submissions/1508202594/){:target="_blank"}

# 설명
1. n개의 정수로 이루어진 [1, n] 범위의 정수가 한 번씩 들어있는 A와 B의 위치 별 이전 값까지의 공통 값이 발생한 갯수를 배열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 A의 길이를 저장한 변수이다.
- counts는 각 숫자의 갯수를 계산해서 넣을 배열로, $length + 1$ 크기의 정수 배열로 초기화한다.
- result는 공통 값이 발생한 갯수를 저장할 배열로, length 크기의 정수 배열로 초기화한다.
- common은 공통 발생한 값을 계산하기 위한 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- counts의 A[i]번째 값과 B[i]번째 값을 증가시키고, 각 위치의 값이 2인 경우 해당 위치까지 A와 B에 공통으로 발생한 값이므로 common을 증가시켜준다.
- result[i]에 common을 넣어 현재 위치까지 공통으로 값이 발생한 갯수를 넣어준다.

4. 반복이 완료되면 완성된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindThePrefixCommonArrayOfTwoArrays.java){:target="_blank"}에서 확인 가능합니다.