---
title: "Leetcode Java Add Binary"
excerpt: "Leetcode - 'Add Binary' 문제 Java 풀이"
last_modified_at: 2021-06-17T18:00:00
header:
  image: /assets/images/leetcode/add-binary.png
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
[Link](https://leetcode.com/problems/add-binary/){:target="_blank"}

# 코드
```java
class Solution {

  public String addBinary(String a, String b) {
    StringBuilder sb = new StringBuilder();
    int aIdx = a.length() - 1;
    int bIdx = b.length() - 1;
    int carry = 0;
    while(aIdx >= 0 || bIdx >= 0) {
      int sum = carry;
      if (aIdx >= 0) {
        sum += a.charAt(aIdx--) - '0';
      }
      if (bIdx >= 0) {
        sum += b.charAt(bIdx--) - '0';
      }
      sb.append(sum % 2);
      carry = sum / 2;
    }
    return (carry == 1 ? sb.append(carry) : sb).reverse().toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/508719599/){:target="_blank"}

# 설명
1. 주어진 두 이진수로 이루어진 문자열 a와 b를 더한 값을 문자열로 반환하는 문제이다.

2. 주어진 문제를 해결하기 위해 기본 변수를 정의한다.
- 주어진 문자열 a와 b를 합친 결과를 저장할 변수 sb를 정의한다.
  - 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.
- 주어진 문자열 a와 b를 역순으로 반복하기 위해 aIdx와 bIdx를 각 문자열의 길이에서 1을 뺀 값으로 정의한다.
- 두 이진 문자열의 합이 2가 넘어 앞 자리가 증가해야 하는 경우(올림의 경우)를 위해 변수 carry를 정의한다.

3. aIdx와 bIdx가 하나라도 0 이상일 때 까지 반복하여 주어진 문자열 a와 b의 합을 계산한다.
- 두 문자열 a와 b의 각 자릿수를 더하기 위해 sum 변수를 정의하고, 해당 값은 직전 값의 올림 값인 carry로 초기화 한다.
- aIdx가 0 이상일 경우, sum에 a의 aIdx번째 값을 더해준다.
- bIdx가 0 이상일 경우, sum에 b의 bIdx번째 값을 더해준다.
  - 위의 두 문자의 정수 값을 사용할 때 char의 int 값은 Ascii code의 값이므로, '0'을 빼서 해당 문자의 정수 값을 구하여 사용한다.
- 위에서 구해진 sum을 이용하여 변수 sb에 $sum \mod 2$의 값을 추가하고, carry에는 $\frac{sum}{2}$의 값을 넣어주어 다음 자리의 계산에 활용한다.

4. 반복이 종료되고 carry가 1일 경우 변수 sb에 carry값을 추가하고, 그렇지 않은 경우 변수 sb 그대로 문자열을 뒤집어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PlusOne.java){:target="_blank"}에서 확인 가능합니다.