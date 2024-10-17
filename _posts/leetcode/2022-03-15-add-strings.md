---
title: "Leetcode Java Add Strings"
excerpt: "Leetcode - 'Add Strings' 문제 Java 풀이"
last_modified_at: 2022-03-15T12:00:00
header:
  image: /assets/images/leetcode/add-strings.png
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
[Link](https://leetcode.com/problems/add-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public String addStrings(String num1, String num2) {
    StringBuilder sb = new StringBuilder();
    int num1Length = num1.length() - 1;
    int num2Length = num2.length() - 1;
    int carry = 0;
    while (num1Length >= 0 || num2Length >= 0) {
      int n1 = num1Length >= 0 ? num1.charAt(num1Length--) - '0' : 0;
      int n2 = num2Length >= 0 ? num2.charAt(num2Length--) - '0' : 0;
      sb.append((n1 + n2 + carry) % 10);
      carry = (n1 + n2 + carry) / 10;
    }
    if (carry > 0) {
      sb.append(carry);
    }
    return sb.reverse().toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/660190591/){:target="_blank"}

# 설명
1. 주어진 두 문자열 num1과 num2은 숫자를 문자로 저장한 변수들로, 두 값의 합을 문자열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sb는 두 값의 합을 넣기 위한 변수로, StringBuilder로 정의한다.
  - 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.
- num1Length와 num2Length는 num1과 num2의 마지막 위치를 커서처럼 사용하기 위한 변수로, 각 길이의 1을 뺀 값으로 넣어준다.
- carry는 두 값의 합이 10을 넘길 경우 다음 위치 값의 합에 더해줄 변수로, 0으로 초기화한다.

3. num1Length와 num2Length 둘 중 하나라도 0보다 큰 경우 아래를 반복한다.
- num1Length가 0보다 큰 경우, n1에 num1의 num1Length번째 값을 넣고 아니면 0을 넣어준 후 num1Length를 감소시킨다.
- num2Length가 0보다 큰 경우, n2에 num2의 num2Length번째 값을 넣고 아니면 0을 넣어준 후 num2Length를 감소시킨다.
- sb에 $n1 + n2 + carry$의 1자리 값을 넣어준다.
- carry에 $n1 + n2 + carry$의 10자리 값을 넣어준다.

4. 반복이 완료되면 carry가 0보다 큰 경우, sb에 carry를 넣어준다.

5. 역순으로 합을 계산하였으므로, sb를 reverse() 메소드를 사용하여 반전시킨 후 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AddStrings.java){:target="_blank"}에서 확인 가능합니다.