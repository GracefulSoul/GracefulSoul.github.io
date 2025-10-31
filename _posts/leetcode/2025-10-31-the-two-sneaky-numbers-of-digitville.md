---
title: "Leetcode Java The Two Sneaky Numbers of Digitville"
excerpt: "Leetcode - 'The Two Sneaky Numbers of Digitville' 문제 Java 풀이"
last_modified_at: 2025-10-31T17:50:00
header:
  image: /assets/images/leetcode/the-two-sneaky-numbers-of-digitville.png
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
[Link](https://leetcode.com/problems/the-two-sneaky-numbers-of-digitville/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] getSneakyNumbers(int[] nums) {
    int n = nums.length - 2;
    int max = 0;
    int[] counts = new int[n];
    for (int num : nums) {
      if (max < ++counts[num]) {
        max = counts[num];
      }
    }
    int index = 0;
    int[] result = new int[2];
    for (int i = 0; i < counts.length; i++) {
      if (counts[i] == max) {
        result[index++] = i;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/the-two-sneaky-numbers-of-digitville/submissions/1816690927/){:target="_blank"}

# 설명
1. 가장 많이 발생한 두 숫자를 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- n은 값의 최대 범위를 저장하기 위한 변수로, 가능한 최댓값인 $nums.length - 2$으로 초기화한다.
- max는 가장 많이 발생한 값의 갯수를 저장할 변수로, 0으로 초기화한다.
- counts는 가장 많이 발생한 값의 갯수를 계산하기 위한 배열로, n 길이의 정수 배열로 초기화한다.
  - nums의 값들을 반복하여 max에 가장 많이 발생한 갯수와 counts 배열에 숫자별 갯수를 계산한다.
- index는 결과 값을 저장할 위치 변수로, 0으로 초기화한다.
- result는 결과 값을 저장할 배열로, 2 크기의 정수 배열로 초기화한다.

3. counts[i]의 값이 max와 동일한 경우, result에 순차적으로 해당 값을 넣어준다.

4. 반복이 완료되어 가장 많이 발생한 두 값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TheTwoSneakyNumbersOfDigitville.java){:target="_blank"}에서 확인 가능합니다.