---
title: "Leetcode Java Maximum Difference Between Even and Odd Frequency I"
excerpt: "Leetcode - 'Maximum Difference Between Even and Odd Frequency I' 문제 Java 풀이"
last_modified_at: 2025-06-10T19:30:00
header:
  image: /assets/images/leetcode/maximum-difference-between-even-and-odd-frequency-i.png
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
[Link](https://leetcode.com/problems/maximum-difference-between-even-and-odd-frequency-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxDifference(String s) {
    int[] counts = new int[26];
    for (char c : s.toCharArray()) {
      counts[c - 'a']++;
    }
    int odd = Integer.MIN_VALUE;
    int even = Integer.MAX_VALUE;
    for (int count : counts) {
      if (count != 0) {
        if (count % 2 == 1) {
          odd = Math.max(odd, count);
        } else {
          even = Math.min(even, count);
        }
      }
    }
    return odd - even;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-difference-between-even-and-odd-frequency-i/submissions/1659589581/){:target="_blank"}

# 설명
1. 문자열 s에서 홀수번 발생한 문자와 짝수번 발생한 문자의 차이가 가장 큰 값을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 문자열 s 내 문자의 갯수를 계산하기 위한 변수로, 정수 배열로 초기화 후 s의 각 문자를 순차적으로 반복하여 갯수를 넣어준다.
- odd와 even은 홀수번, 짝수번 발생한 문자의 갯수를 계산하기 위한 변수로, 정수의 가장 작은 값과 큰 값으로 초기화한다.

3. counts를 순차적으로 count에 넣어 아래를 반복한다.
- count가 0이 아닌 경우만 아래를 수행한다.
  - count가 홀수인 경우, odd에 odd와 count 중 큰 값을 넣어준다.
  - count가 짝수인 경우, even에 even과 count 중 작은 값을 넣어준다.

4. 3번을 통해 가장 큰 홀수 값인 odd와 가장 작은 짝수 값인 even의 차잇값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumDifferenceBetweenEvenAndOddFrequencyI.java){:target="_blank"}에서 확인 가능합니다.