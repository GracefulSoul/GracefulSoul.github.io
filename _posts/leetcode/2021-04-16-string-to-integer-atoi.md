---
title: "Leetcode Java String to Integer (atoi)"
excerpt: "Leetcode String to Integer (atoi) Java 풀이"
last_modified_at: 2021-04-16T18:10:00
header:
  image: /assets/images/leetcode/string-to-integer-atoi.png
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
[Link](https://leetcode.com/problems/string-to-integer-atoi/)

# 코드
```java
class Solution {

  public int myAtoi(String s) {
    int result = 0;
    if (s.length() == 0) {
      return result;
    }
    int idx = getBeginning(s);
    if (idx == s.length()) {
      return result;
    }
		int sign = 1;
    if (s.charAt(idx) == '+' || s.charAt(idx) == '-') {
      sign = s.charAt(idx++) == '-' ? -1 : 1;
    }
    while (idx < s.length() && s.charAt(idx) >= '0' && s.charAt(idx) <= '9') {
      if (isOverflow(result, s.charAt(idx))) {
        return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
      }
      result = result * 10 + s.charAt(idx++) - '0';
    }
    return result * sign;
  }

  private int getBeginning(String s) {
    int idx = 0;
    while (idx < s.length() && s.charAt(idx) == ' ') {
      idx++;
    }
    return idx;
  }

  private boolean isOverflow(int result, char c) {
    return result > Integer.MAX_VALUE / 10
        || (result == Integer.MAX_VALUE / 10 && c - '0' > Integer.MAX_VALUE % 10);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/481300277/)

# 설명
1. 주어진 문자열 s는 0부터 1000까지 길이이므로 s의 길이가 0일 경우, 0을 그대로 주어진 문제의 결과로 반환한다.

2. 주어진 문자열 s의 공백을 확인하여 숫자열 탐색의 시작 index를 확인하여 idx 변수에 저장한다.
  - 공백 문자열의 길이는 주어진 문자열 s보다 작고, s의 idx번째 문자가 공백 문자열의 경우만 idx를 점층적으로 증가시킨다.
  - 만일 idx가 s의 길이와 같거나 공백이 아닌 문자열이 탐색되었을 경우, 반복을 중지하고 idx를 숫자열 탐색의 시작 index로 반환한다.

3. 숫자열 탐색의 시작 index인 idx가 주어진 문자열 s의 길이와 같을 경우, 0을 그대로 주어진 문제의 결과로 반환한다.
	- 주어진 문자열 s가 공백으로만 이루어진 문자열인 경우이다.

4. 주어진 문자열 s의 idx번째 문자가 +나 -인 경우 idx를 증가시키고, -인 경우만 sign을 -1로 변경하여 음수 결과를 반환할 수 있도록한다.

5. 주어진 문자열 s을 idx번째 index부터 각 문자가 0 ~ 9 사이의 숫자인 경우만 탐색한다.
	- 만일 결과로 반환할 result가 int형의 최댓값의 $\frac{1}{10}$인 214,748,364를 초과 할 경우이거나, result가 214,748,364이고 주어진 문자열 s의 idx번째 문자가 7보다 클 경우 int형의 최댓값과 최솟값을 초과하므로 Overflow 처리한다.
		- Character형인 c를 '0'으로 빼면 Ascii 값 기준으로 해당 값의 숫자로 반환된다.
	- 위의 Overflow 처리된 경우, sign이 1이면 int형의 최댓값인 2,147,483,647를 주어진 문제의 결과로 반환한다.
	- sign이 -1이면 int형의 최솟값인 -2,147,483,648을 주어진 문제의 결과로 반환한다.
	- Overflow 처리가 되지 않은 경우, result에 reulst * 10과 주어진 문자열 s의 idx번째 문자열의 ascii 코드값에 '0'의 ascii 코드값을 뺀 값을 저장하고 반복을 계속 수행한다.

6. 반복이 끝나면 결과로 반환할 result에 음수/양수를 구분할 sign값을 곱하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StringToIntegerAtoi.java)에서 확인 가능합니다.