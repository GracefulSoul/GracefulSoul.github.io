---
title: "Leetcode Java N-th Tribonacci Number"
excerpt: "Leetcode N-th Tribonacci Number Java"
last_modified_at: 2024-04-24T18:20:00
header:
  image: /assets/images/leetcode/n-th-tribonacci-number.png
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
[Link](https://leetcode.com/problems/n-th-tribonacci-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int tribonacci(int n) {
    if (n < 2) {
      return n;
    } else {
      int result = 1;
      for (int i = 0, j = 1; n > 2; n--) {
        int temp = i + j + result;
        i = j;
        j = result;
        result = temp;
      }
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/n-th-tribonacci-number/submissions/1240654557/){:target="_blank"}

# 설명
1. n번째 [Tribonacci sequence](https://en.wikipedia.org/wiki/Generalizations_of_Fibonacci_numbers#Tribonacci_numbers){:target="_blank"} 값을 반환하는 문제이다.
- n번째 Tribonacci sequence는 T<sub>n</sub>로 나타낸다.
- $T<sub>0</sub> = 0, T<sub>1</sub> = 1, T<sub>2</sub> = 1$이다.
- $T<sub>n + 3</sub> = T<sub>n</sub> + T<sub>n + 1</sub> + T<sub>n + 2</sub>$를 만족한다.

2. n이 2 미만인 경우, n을 그대로 주어진 문제의 결과로 반환한다.

3. n이 2 이상인 경우, 아래를 수행한다.
- result는 결과를 저장할 변수로, 1로 초기화한다.
- i와 j는 각각 0과 1로 초기화하여 n의 값이 2보다 클 때까지 아래를 수행하고 n을 감소시킨다.
  - temp에 $i + j + result$를 임시로 넣어준다.
  - i에 j를, j에 result를, result에 temp를 넣어 값을 바꾸어준다.

4. 반복이 완료되어 계산된 result를 주어진 문제의 결과로 반화한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NthTribonacciNumber.java){:target="_blank"}에서 확인 가능합니다.