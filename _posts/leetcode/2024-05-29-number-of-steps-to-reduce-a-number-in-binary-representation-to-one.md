---
title: "Leetcode Java Number of Steps to Reduce a Number in Binary Representation to One"
excerpt: "Leetcode Number of Steps to Reduce a Number in Binary Representation to One Java"
last_modified_at: 2024-05-29T18:40:00
header:
  image: /assets/images/leetcode/number-of-steps-to-reduce-a-number-in-binary-representation-to-one.png
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
[Link](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-in-binary-representation-to-one/){:target="_blank"}

# 코드
```java
class Solution {

  public int numSteps(String s) {
    int result = 0;
    int carry = 0;
    for (int i = s.length() - 1; i > 0; i--) {
      result++;
      if (s.charAt(i) - '0' + carry == 1) {
        carry = 1;
        result++;
      }
    }
    return result + carry;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-in-binary-representation-to-one/submissions/1271263583/){:target="_blank"}

# 설명
1. 이진법 문자열 s를 이용하여 아래 규칙에 따라 1로 감소시키기 위한 횟수를 구하는 문제이다.
- 현재 숫자가 짝수이면 2로 나눈다.
- 현재 숫자가 홀수이면 1을 더한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 횟수를 저장할 변수로, 0으로 초기화한다.
- carry는 증가하는 값을 저장할 변수로, 0으로 초기화한다.

3. s의 길이보다 1 작은 값부터 0 초과일 때까지 i를 감소시키며 아래를 반복한다.
- 값이 짝수/홀수인지 여부를 제외하고 한 번을 수행하므로 result를 증가시킨다.
- s의 i번째 문자를 숫자로 변환한 값과 carry를 더한 값이 1인 홀수인 경우 두 번 수행하므로, carry에 1을 넣어주고 result를 증가시킨다.
  - 홀수인 경우, 1을 증가시키고 짝수를 만들어 2를 나누므로 2번 수행한다.

4. 반복이 완료되면 마지막 이전까지 계산된 수행 횟수인 result와 carry가 1인 경우 다시 2로 나누어야 하므로 carry를 더한 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfStepsToReduceANumberInBinaryRepresentationToOne.java){:target="_blank"}에서 확인 가능합니다.