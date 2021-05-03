---
title: "Leetcode Java Generate Parentheses"
excerpt: "Leetcode Generate Parentheses Java 풀이"
last_modified_at: 2021-05-03T20:10:00
header:
  image: /assets/images/leetcode/generate-parentheses.png
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
[Link](https://leetcode.com/problems/generate-parentheses/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> generateParenthesis(int n) {
    List<String> list = new ArrayList<>();
    this.generate(list, "", 0, 0, n);
    return list;
  }

  private void generate(List<String> list, String str, int left, int right, int n) {
    if (str.length() == n * 2) {
      list.add(str);
      return;
    }
    if (left < n) {
      this.generate(list, this.appendString(str, '('), left + 1, right, n);
    }
    if (right < left) {
      this.generate(list, this.appendString(str, ')'), left, right + 1, n);
    }
  }

  private String appendString(String str, char c) {
    return new StringBuilder(str).append(c).toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/488294744/){:target="_blank"}

# 설명
1. 주어진 정수 n의 크기만큼의 올바른 형식의 소괄호 모양을 만들기 위해서 최대 크기부터 재귀 호출을 사용한다.
  - 올바른 형식의 최대 크기 소괄호 모양을 만들기 위해서는 '(' 문자열이 n개부터 시작하는 경우이다.
  - 올바른 형식의 최소 크기 소괄호 모양을 만들기 위해서는 '(' 문자열이 1개부터 시작하는 경우이다.

2. 만일 올바른 형식의 소괄호 모양을 저장하는 str의 크기가 주어진 정수 n의 2배일 경우, 결과를 저장하는 배열 list에 추가한다.
  - 올바른 형식의 소괄호 문자열은 항상 '(' 문자열과 ')' 문자열의 갯수가 같으므로, 최대 문자열의 길이는 항상 $n \times 2$이어야 한다.

3. 변수 left가 주어진 숫자 n보다 작은 경우, '(' 문자를 문자열 str에 이어쓰고 $left + 1$을 하여 재귀 호출을 반복한다.
  - 이 경우, 1번에서 이야기한 '(' 문자열이 n개부터 시작하는 문자열을 만들기 시작한다.

4. 변수 right가 변수 left보다 작은 경우, ')'문자를 문자열 str에 이어쓰고 $rigth + 1$을 하여 재귀 호출을 반복한다.
  - 이 경우, 1번에서 이야기한 '(' 문자열이 1개부터 시작하는 문자열을 만들기 시작한다.

5. 재귀호출이 완료되면 결과를 저장하는 배열 list를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GenerateParentheses.java){:target="_blank"}에서 확인 가능합니다.