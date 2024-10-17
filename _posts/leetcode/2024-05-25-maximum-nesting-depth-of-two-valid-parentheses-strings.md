---
title: "Leetcode Java Maximum Nesting Depth of Two Valid Parentheses Strings"
excerpt: "Leetcode Medium - 'Maximum Nesting Depth of Two Valid Parentheses Strings' 문제 Java 풀이"
last_modified_at: 2024-05-25T12:00:00
header:
  image: /assets/images/leetcode/maximum-nesting-depth-of-two-valid-parentheses-strings.png
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
[Link](https://leetcode.com/problems/maximum-nesting-depth-of-two-valid-parentheses-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] maxDepthAfterSplit(String seq) {
    int length = seq.length();
    int[] result = new int[length];
    for (int i = 0, count = 0; i < length; i++) {
      if (seq.charAt(i) == '(') {
        result[i] = ++count % 2;
      } else {
        result[i] = count-- % 2;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-nesting-depth-of-two-valid-parentheses-strings/submissions/1267093088/){:target="_blank"}

# 설명
1. 소괄호로 구성된 seq를 이용하여 아래의 규칙을 따른 결과를 반환하는 문제이다.
- 유효한 괄호 문자열은 빈 문자열이거나, A와 B가 연결된 AB, (A)로 구성된 문자열이다.
- 길이인 depth(S)는 아래의 규칙을 따른다.
  - depth("") = 0
  - depth(A + B) = max(depth(A), depth(B))
  - depth("(" + A + ")")  = 1 + depth(A)
- seq를 VPS를 만족하는 A와 B 두 문자열로 구성하여 max(depth(A), depth(B))의 값이 최소가 되도록 한 문자열을 선택한다.
  - seq의 길이와 A와 B 문자열의 길이는 동일하다.
- 결과의 i번째 값은 seq의 i번째 문자가 A에 포함되어 있으면 0을, 아니면 1을 넣어준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 seq의 길이를 저장한 변수이다.
- result는 결과 값을 저장할 변수로, length 길이의 정수 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키고, '('의 갯수를 계산할 count는 0으로 초기화하여 아래를 반복한다.
- seq의 i번째 문자가 '(' 문자인 경우, result[i]에 count를 증가시키고 해당 값을 2로 나눈 나머지 값을 넣어준다.
- seq의 i번째 문자가 ')' 문자인 경우, result[i]에 count를 2로 나눈 나머지 값을 넣고 count를 감소시킨다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 해설
- max(depth(A), depth(B))의 값이 최소가되기 위해서 depth를 각각 나눠줘야 한다.
- depth를 분리하기 위해서 홀수 괄호는 A에, 짝수 괄호는 B에 구성한다.
- 위로 구성된 결과에 따라서 count가 홀수이면 A에 포함되었다고 판단할 수 있다.
  - A를 짝수, B를 홀수로 구성하게 되면 count 또한 짝수이면 A에 포함된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumNestingDepthOfTwoValidParenthesesStrings.java){:target="_blank"}에서 확인 가능합니다.