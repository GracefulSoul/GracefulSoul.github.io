---
title: "Leetcode Java Perfect Number"
excerpt: "Leetcode - 'Perfect Number' 문제 Java 풀이"
last_modified_at: 2022-05-26T19:00:00
header:
  image: /assets/images/leetcode/perfect-number.png
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
[Link](https://leetcode.com/problems/perfect-number/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkPerfectNumber(int num) {
    if (num == 1) {
      return false;
    }
    int sum = 1;
    for (int idx = 2; idx * idx <= num; idx++) {
      if (num % idx == 0) {
        sum += idx + (num / idx);
      }
    }
    return sum == num;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/707547273/){:target="_blank"}

# 설명
1. num이 완전수로 이루어졌는지 검증하는 문제이다.
- 완전수는 양의 제수의 합과 동일한 양의 정수로, 정수 x의 제수는 x를 균등하게 나눌 수 있는 정수이다.
- 예를 들어, $28 = 1 + 2 + 4 + 7 + 14$는 완전수이다.

2. nums이 1인 경우 자기 자신을 균등하게 나눌 수있는 양의 정수가 없으므로, 주어진 문제의 결과로 false를 반환한다.

3. sum은 완전수를 검증하기 위한 합계를 위한 변수로, 첫 값인 1로 초기화한다.

4. 2부터 idx의 제곱이 sum보다 작을 때 까지 idx를 증가하여 아래를 검증한다.
- num을 idx로 나머지 없이 나눌 수 있을 경우, sum에 idx와 $\frac{num}{idx}$의 합을 더해준다.
  - idx와 $\frac{num}{idx}$의 곱은 num으로, num의 두 제수의 합을 의미한다.

5. 반복이 완료된 경우 sum과 num이 동일한지 검증하여, 해당 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PerfectNumber.java){:target="_blank"}에서 확인 가능합니다.