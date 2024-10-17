---
title: "Leetcode Java Reverse Integer"
excerpt: "Leetcode - 'Reverse Integer' 문제 Java 풀이"
last_modified_at: 2021-04-15T21:10:00
header:
  image: /assets/images/leetcode/zigzag-conversion.png
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
[Link](https://leetcode.com/problems/zigzag-conversion/){:target="_blank"}

# 코드
```java
class Solution {

  public int reverse(int x) {
    int result = 0;
    while (x != 0) {
      int temp = result * 10 + x % 10;
      if (temp / 10 != result) {
        return 0;
      } else {
        result = temp;
        x /= 10;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/480942023/){:target="_blank"}

# 설명
1. 주어진 정수 x를 반대로 전환한 결과값을 저장할 result 변수를 선언한다.

2. 반복문을 통해 x가 0이 될 때까지 반복을 통해 주어진 정수를 역전시킨다.
- 임시 정수로 사용되는 temp 변수를 선언하여 $result\times10 + \frac{x}{10}$을 통해 정수를 역순으로 생성해준다.
- $\frac{x}{10}$을 통해 주어진 정수의 마지막 자리를 첫 자리로 전환한다. 단 마지막 숫자열이 0인 경우, temp가 0이 되므로 무시된다.
- $result\times10$을 통해 역전시키는 정수의 자릿수를 올려준다.

3. 만일 임시 정수로 사용되는 temp변수에 10으로 나눈 값과 result의 값이 다른 경우, 주어진 문제의 결과로 0을 반환한다.
- $result\times10$을 통해 int형의 최솟값(-2,147,483,648)과 최댓값(2,147,483,647)을 돌파할 경우, 값이 초기화되는 점을 활용한다. ($-2147483648\times10{=}0$, $2147483648\times10{=}-10$)
- 위의 이유로 $\frac{temp}{10}의 결과값과 result의 값이 같지 않다면, int형의 범위를 넘어섰으므로 문제에서 예외 케이스로 주어진 경우를 만족하여 0을 결과로 반환한다.

4. 3번의 경우가 아닌 경우에는 결과값을 저장하는 result 변수에 임시 정수로 사용되는 temp 변수의 값을 주입하고, x값에 $\frac{x}{10}$의 몫을 저장하고 반복문을 계속 수행한다.

5. 반복문이 종료되면 주어진 정수 x를 반대로 전환한 결과값을 저장한 result 변수의 값을 주어진 문제의 결과로 반환한다.
  

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseInteger.java){:target="_blank"}에서 확인 가능합니다.