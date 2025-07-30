---
title: "Leetcode Java Longest Subarray With Maximum Bitwise AND"
excerpt: "Leetcode - 'Longest Subarray With Maximum Bitwise AND' 문제 Java 풀이"
last_modified_at: 2025-07-30T20:30:00
header:
  image: /assets/images/leetcode/longest-subarray-with-maximum-bitwise-and.png
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
[Link](https://leetcode.com/problems/longest-subarray-with-maximum-bitwise-and/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestSubarray(int[] nums) {
    int result = 1;
    int max = Integer.MIN_VALUE;
    for (int num : nums) {
      max = Math.max(max, num);
    }
    int temp = 0;
    for (int num : nums) {
      if (num == max) {
        temp++;
      } else {
        result = Math.max(result, temp);
        temp = 0;
      }
    }
    return Math.max(result, temp);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-subarray-with-maximum-bitwise-and/submissions/1717022012/){:target="_blank"}

# 설명
1. nums 내 아래의 조건을 만족하는 최대 길이를 구하는 문제이다.
- 모든 부분 배열의 AND 비트 연산 값의 최댓값으로 이루어진 값으로 이루어진 값들의 연속된 최대 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최대 길이를 저장할 변수로, 최소 길이인 1으로 초기화한다.
- max는 최댓값을 구하기 위한 변수로, 정수의 최솟값으로 초기화 후 nums의 각 값을 반복하여 최댓값을 넣어준다.
- temp는 최대 길이를 저장하기 위한 임시 변수로, 0으로 초기화한다.

3. nums의 각 값을 num에 순차적으로 넣어 아래를 반복한다.
- num이 max와 동일한 경우, temp를 증가시킨다.
- 위의 경우가 아니라면, result에 result와 temp 중 큰 값인 최대 길이를 저장 후 temp를 0으로 초기화한다.

4. 이전까지 저장된 최대 길이인 result와 마지막으로 계산된 최대 길이인 temp 중 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestSubarrayWithMaximumBitwiseAND.java){:target="_blank"}에서 확인 가능합니다.