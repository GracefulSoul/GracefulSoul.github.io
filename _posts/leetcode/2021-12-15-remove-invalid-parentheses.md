---
title: "Leetcode Java Remove Invalid Parentheses"
excerpt: "Leetcode Remove Invalid Parentheses Java 풀이"
last_modified_at: 2021-12-15T13:00:00
header:
  image: /assets/images/leetcode/remove-invalid-parentheses.png
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
[Link](https://leetcode.com/problems/remove-invalid-parentheses/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> removeInvalidParentheses(String s) {
    List<String> result = new ArrayList<>();
    this.recursive(s, result, new char[] { '(', ')' }, 0, 0);
    return result;
  }

  private void recursive(String s, List<String> result, char[] check, int x, int y) {
    int count = 0;
    int i = x;
    while (i < s.length() && count >= 0) {
      if (s.charAt(i) == check[0]) {
        count++;
      }
      if (s.charAt(i) == check[1]) {
        count--;
      }
      i++;
    }
    if (count >= 0) {
      String reverse = new StringBuilder(s).reverse().toString();
      if (check[0] == '(') {
        this.recursive(reverse, result, new char[] { ')', '(' }, 0, 0);
      } else {
        result.add(reverse);
      }
    } else {
      i--;
      for (int j = y; j <= i; j++) {
        if (s.charAt(j) == check[1] && (j == y || s.charAt(j - 1) != check[1])) {
          this.recursive(s.substring(0, j) + s.substring(j + 1, s.length()), result, check, i, j);
        }
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/602098345/){:target="_blank"}

# 설명
1. 주어진 문자열 s에 괄호가 유효하지(정상적으로 열고 닫지) 않는 문자열로 구성되어 있으면, 최소의 괄호를 제거하여 괄호가 유효한 문자열을 모두 만들어 반환하는 문제이다.

2. 모든 괄호가 유효한 문자열을 넣을 컬렉션인 result를 정의하고, 배열의 정순인 "(", ")" 문자열 순서로 재귀 호출을 수행하여 result에 모든 결과를 넣어준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- count는 유효하지 않은 괄호의 개수를 파악하기 위한 변수로, 0으로 초기화한다.
- i는 문자열 s를 탐색하기 위한 시작 위치인 변수로, 주어진 변수 x로 초기화한다.

4. 문자열 s의 i번째 문자부터 끝까지 반복을 통해 탐색하여 아래를 수행한다.
- 문자열 s의 i번째 문자가 check의 첫 번째 문자인 경우, count를 증가시킨다.
- 문자열 s의 i번째 문자가 check의 두 번째 문자인 경우, count를 감소시킨다.
- 마지막으로 i를 증가시키고 반복을 계속한다.

5. count가 0 이상인 경우, 유효하지 않은 괄호가 존재하므로 아래를 수행한다.
- 문자열 s를 거꾸로 반전시켜서 reverse에 저장한다.
- check의 첫 번째 문자가 괄호의 시작인 '('인 경우, check를 반대로 바꾸어 재귀 호출을 수행한다.
- check의 첫 번째 문자가 괄호의 종료인 ')'인 경우, result에 reverse 문자열을 넣어준다.

6. count가 0인경우, 문자열의 괄호를 검증하기 위해 아래를 수행한다.
- 해당 검증을 수행하기 위해 i를 감소시킨다.
- y부터 i 이전까지 반복을 수행한다.
- s의 j번째 문자가 check의 두 번째 문자이면서, j와 y가 같거나 s의 $j - 1$번째 문자가 check의 두 번째 문자가 아닌 경우에는 j번째 문자만 s에서 제외하고 x에 i를, y에 j를 넣어 재귀 호출을 수행한다.

7. 재귀 호출이 완료되서 모든 가능한 문자열을 result에 넣어지면 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveInvalidParentheses.java){:target="_blank"}에서 확인 가능합니다.