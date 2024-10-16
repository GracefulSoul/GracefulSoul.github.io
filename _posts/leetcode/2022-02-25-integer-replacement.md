---
title: "Leetcode Java Integer Replacement"
excerpt: "Leetcode Integer Replacement Java 풀이"
last_modified_at: 2022-02-25T13:00:00
header:
  image: /assets/images/leetcode/integer-replacement.png
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
[Link](https://leetcode.com/problems/integer-replacement/){:target="_blank"}

# 코드
```java
class Solution {

  public int integerReplacement(int n) {
    int count = 0;
    while (n > 1) {
      if ((n & 1) != 0) {
        n += (n == 3 || ((n >> 1) & 1) == 0) ? -1 : 1;
        count++;
      }
      n >>>= 1;
      count++;
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/648436492/){:target="_blank"}

# 설명
1. 주어진 정수 n을 이용하여 아래의 규칙을 이용하여 1로 변환하는 가장 작은 횟수를 구하는 문제이다.
- n이 짝수인 경우, n을 2로 나누어준다.
- n이 홀수인 경우, n에 1을 빼거나 더하여 짝수로 변환한다.

2. 변환 횟수를 저장할 count를 정의하고, 0으로 초기화한다.

3. n이 1보다 클 때 까지 반복하여 아래를 수행한다.
- n 과 1의 AND(&) 비트 연산의 결과가 0이 아닌 경우 홀수이므로, 아래를 수행한다.
  - n의 비트를 우측으로 한 칸 이동한 결과와 1의 AND(&) 비트 연산을 수행한 결과가 0인 경우와 특이 케이스인 n이 3인 경우는 n을 감소시키는 것이 횟수를 줄이는 방법이므로, n에 1을 빼준다.
  - 위의 경우가 아닌 경우, n에 1을 증가시킨다.
  - 예를 들어 n이 5(101)인 경우, 1을 더하면 6 -> 3 -> 2 -> 1로 3번, 1을 빼면 4 -> 2 -> 1로 2번이 된다.
  - 다른 예로 n이 3(11)인 경우 1의 AND(&) 비트 연산의 결과가 1이지만, 1을 더하면 4 -> 2 -> 1로 2번, 1을 빼면 2 -> 1로 1번이 되므로 예외 처리를 수행한다.
  - 마지막으로 홀수를 짝수로 변경했으므로, count를 증가시킨다.
- n의 비트를 우측으로 두 칸 이동을 시킨다.
  - n /= 2와 기능은 동일하지만, overflow를 방지할 수 있다.
- 짝수를 2로 나누었으므로, count를 증가시킨다.

4. 반복이 완료되면 n을 1로 변환하는 가장 작은 횟수를 저장한 count를 주어진 문제의 결과로 반환한다.
  
# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IntegerReplacement.java){:target="_blank"}에서 확인 가능합니다.