---
title: "Leetcode Java Largest Combination With Bitwise AND Greater Than Zero"
excerpt: "Leetcode - 'Largest Combination With Bitwise AND Greater Than Zero' 문제 Java 풀이"
last_modified_at: 2024-11-07T18:10:00
header:
  image: /assets/images/leetcode/largest-combination-with-bitwise-and-greater-than-zero.png
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
[Link](https://leetcode.com/problems/largest-combination-with-bitwise-and-greater-than-zero/){:target="_blank"}

# 코드
```java
class Solution {

  public int largestCombination(int[] candidates) {
    int result = 0;
    for (int i = 0; i < 32; i++) {
      int count = 0;
      for (int candidate : candidates) {
        if ((candidate & (1 << i)) != 0) {
          count++;
        }
      }
      result = Math.max(result, count);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-if-array-can-be-sorted/submissions/1444662145/){:target="_blank"}

# 설명
1. candidates의 AND(&) 비트 연산의 결과가 가장 크게 되는 부분 배열의 크기가 가장 큰 값을 찾는 문제이다.

2. result는 부분 배열의 크기를 저장할 변수로, 0으로 초기화한다.

3. 0부터 정수 길이의 최대 길이보다 작은 32 미만까지 i를 증가시키면서 아래를 반복한다.
- count는 해당되는 갯수를 계산하기 위한 변수로 0으로 초기화한다.
- candidates의 모든 값을 순차적으로 candidate에 넣고 아래를 반복한다.
  - candidate와 1을 i번 좌측으로 이동 시킨 비트의 값을 AND(&) 비트 연산한 결과가 0이 아닌 값이 존재하는 경우, count를 증가시킨다.
- result에 이전까지 최대 갯수인 result와 현재 갯수인 count 중 큰 값을 넣어준다.

4. 반복이 완료되면 부분 배열의 크기가 가장 큰 값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestCombinationWithBitwiseANDGreaterThanZero.java){:target="_blank"}에서 확인 가능합니다.