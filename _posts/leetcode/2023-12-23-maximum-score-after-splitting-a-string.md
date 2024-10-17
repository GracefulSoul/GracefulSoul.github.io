---
title: "Leetcode Java Maximum Score After Splitting a String"
excerpt: "Leetcode Easy - 'Maximum Score After Splitting a String' 문제 Java 풀이"
last_modified_at: 2023-12-23T09:10:00
header:
  image: /assets/images/leetcode/maximum-score-after-splitting-a-string.png
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
[Link](https://leetcode.com/problems/maximum-score-after-splitting-a-string){:target="_blank"}

# 코드
```java
class Solution {

  public int maxScore(String s) {
    int zeros = 0;
    int ones = 0;
    int max = Integer.MIN_VALUE;
    for (int i = 0; i < s.length(); i++) {
      if (s.charAt(i) == '0') {
        zeros++;
      } else {
        ones++;
      }
      if (i != s.length() - 1) {
        max = Math.max(zeros - ones, max);
      }
    }
    return max + ones;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-score-after-splitting-a-string/submissions/1126216951/){:target="_blank"}

# 설명
1. s를 두 문자열로 나누어 좌측 문자열의 0의 갯수와 우측 문자열의 1의 갯수가 가장 큰 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 저으이한다.
- zeros와 ones는 0과 1의 수를 저장할 변수로, 둘 다 0으로 초기화한다.
- max는 좌측 문자열의 0의 갯수에서 1의 갯수를 뺀 값이 가장 큰 값을 저장할 변수로, 정수의 가장 작은 값으로 초기화한다.

3. 0부터 s의 길이 미만까지 아래를 반복한다.
- s의 i번째 문자가 0인 경우 zeros를 증가시키고 아니면 ones를 증가시킨다.
- i가 마지막 위치가 아닌 경우, max에 $zeros - ones$와 max 중 큰 값을 넣어준다.

4. 반복이 완료되면 $max + ones$를 주어진 문제의 결과로 반환한다.

# 해설
- 좌측의 0의 갯수와 우측의 1의 갯수가 가장 큰 값에 대한 공식은 아래와 같다.
- $MAX(left_zeros + right_ones) = MAX(left_zeros - left_ones + left_ones + right_ones) = MAX(left_zeros - left_ones) + total_ones$
- 위의 공식을 이용하여 MAX(left_zeros - left_ones)를 구한 값에 1의 총 갯수를 더하면 원하는 값이 나오게 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumScoreAfterSplittingAString.java){:target="_blank"}에서 확인 가능합니다.