---
title: "Leetcode Java Factorial Trailing Zeroes"
excerpt: "Leetcode - 'Factorial Trailing Zeroes' 문제 Java 풀이"
last_modified_at: 2021-09-22T07:30:00
header:
  image: /assets/images/leetcode/factorial-trailing-zeroes.png
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
[Link](https://leetcode.com/problems/factorial-trailing-zeroes/){:target="_blank"}

# 코드
```java
class Solution {

  public int trailingZeroes(int n) {
    int count = 0;
    while (n != 0) {
      n /= 5;
      count += n;
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/558846506/){:target="_blank"}

# 설명
1. 주어진 정수 n을 [Factorial](https://en.wikipedia.org/wiki/Factorial)을 사용하여 n! 값 뒷자리에 존재하는 0의 개수를 구하는 문제이다.
- 간단히 주어진 문제를 직관적으로 보면, n! 값 뒷자리에 존재하는 0의 개수는 10이 몇 개 곱해졌는지를 파악하면된다.
- 위의 내용을 깊이 파고들면 $2 \times 5 = 10$이므로 소수인 2는 5!, 10! 이하의 모든 값들에 포함되는 값으로, n! 내에 존재하는 5의 개수만 파악하면 해결 가능한 문제이다.

2. 주어진 정수 n을 이용하여 n! 내 존재하는 5의 개수를 세기 위한 변수인 count를 정의한다.

3. 주어진 정수 n이 0이 되기 전까지 반복하여 count에 5의 개수를 더한다.
- 주어진 정수 n을 5로 나눈 결과를 n에 다시 주입한다.
- count에 n을 더하여 5의 개수를 넣어준다.
  - n!내 5의 개수를 구하는 가장 효율적인 방법은, n에서 5를 계속 나누어 준 몫의 합이 해당 개수가 된다.

4. n! 값 뒤에 존재하는 0의 개수를 넣은 변수 count의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FactorialTrailingZeroes.java){:target="_blank"}에서 확인 가능합니다.