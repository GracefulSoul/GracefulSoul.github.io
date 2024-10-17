---
title: "Leetcode Java Monotone Increasing Digits"
excerpt: "Leetcode - 'Monotone Increasing Digits' 문제 Java 풀이"
last_modified_at: 2022-11-26T10:30:00
header:
  image: /assets/images/leetcode/monotone-increasing-digits.png
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
[Link](https://leetcode.com/problems/monotone-increasing-digits){:target="_blank"}

# 코드
```java
class Solution {

  public int monotoneIncreasingDigits(int n) {
    char[] charArray = String.valueOf(n).toCharArray();
    int end = charArray.length - 1;
    for (int idx = charArray.length - 1; idx > 0; idx--) {
      if (charArray[idx - 1] > charArray[idx]) {
        end = idx - 1;
        charArray[idx - 1]--;
      }
    }
    for (int idx = end + 1; idx < charArray.length; idx++) {
      charArray[idx] = '9';
    }
    return Integer.parseInt(new String(charArray));
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/849858202/){:target="_blank"}

# 설명
1. n의 각 자릿수의 숫자가 점층적으로 증가하는지 확인하여 해당 조건을 만족하지 않는 경우, n보다 작은 숫자 중 가장 큰 조건에 만족하는 숫자를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 정수인 n을 문자의 배열로 변환하여 저장한 변수이다.
- end는 조건을 만족하지 않는 마지막 위치를 저장할 변수로, charArray의 길이보다 1 작은 값으로 초기화한다.

3. chaArray의 길이보다 1 작은 수부터 0 초과까지 idx를 증가시키며 아래를 반복한다.
- charArray의 $idx - 1$번째 문자가 idx번째 문자보다 큰 경우, 조건을 만족하지 않기 때문에 end에 $idx - 1$을 넣고 charArray의 $idx - 1$번째 값을 1 작게 한다.

4. $end + 1$부터 charArray의 길이 미만까지 idx를 증가시키며 각 자리에 9를 넣어 n 미만의 점층적으로 증가하는 가장 큰 숫자를 만들어준다.

5. 반복이 완료되면 charArray를 정수로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MonotoneIncreasingDigits.java){:target="_blank"}에서 확인 가능합니다.