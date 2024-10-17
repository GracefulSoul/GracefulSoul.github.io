---
title: "Leetcode Java Numbers At Most N Given Digit Set"
excerpt: "Leetcode - 'Numbers At Most N Given Digit Set' 문제 Java 풀이"
last_modified_at: 2023-04-16T13:50:00
header:
  image: /assets/images/leetcode/numbers-at-most-n-given-digit-set.png
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
[Link](https://leetcode.com/problems/numbers-at-most-n-given-digit-set){:target="_blank"}

# 코드
```java
class Solution {

  public int atMostNGivenDigitSet(String[] digits, int n) {
    String str = String.valueOf(n);
    int length = str.length();
    int[] dp = new int[length + 1];
    dp[length] = 1;
    for (int i = length - 1; i >= 0; i--) {
      int num = str.charAt(i) - '0';
      for (String digit : digits) {
        if (Integer.parseInt(digit) < num) {
          dp[i] += Math.pow(digits.length, length - i - 1);
        } else if (Integer.parseInt(digit) == num) {
          dp[i] += dp[i + 1];
        }
      }
    }
    for (int i = 1; i < length; i++) {
      dp[0] += Math.pow(digits.length, i);
    }
    return dp[0];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/numbers-at-most-n-given-digit-set/submissions/934539451/){:target="_blank"}

# 설명
1. 작은 값 순으로 저장된 digits 배열을 이용하여 n보다 같거나 작은 값의 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- str은 n을 문자열로 변환한 변수이고, length는 str의 길이를 저장한 변수이다.
- dp는 값의 탐색에 필요한 변수로, $length + 1$ 크기의 정수 배열로 초기화하고 마지막 위치에 1을 넣어준다.

3. $length - 1$부터 0 이상까지 i를 증가시키며 아래를 반복한다.
- num에 str의 i번째 문자를 숫자로 변환하여 digits의 모든 값을 차례대로 digit에 넣어 아래를 반복한다.
  - digit이 num보다 작은 경우 해당 값 아래로 만들 수 있는 모든 값의 갯수를 저장해야 하므로, dp의 i번째 위치에 digits의 길이의 $length - i - 1$승 값을 넣어준다.
  - digit이 num과 동일한 경우, dp의 i번째 위치에 이전에 계산된 숫자의 갯수인 $i + 1$번째 값을 넣어준다.

4. 1부터 length까지 i를 증가시키며 dp의 처음 위치에 digits의 길이의 i승 결과를 더해주고, 해당 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OnlineStockSpan.java){:target="_blank"}에서 확인 가능합니다.