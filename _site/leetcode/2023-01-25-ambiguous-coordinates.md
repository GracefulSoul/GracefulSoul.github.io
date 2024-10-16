---
title: "Leetcode Java Ambiguous Coordinates"
excerpt: "Leetcode Ambiguous Coordinates Java"
last_modified_at: 2023-01-25T19:45:00
header:
  image: /assets/images/leetcode/ambiguous-coordinates.png
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
[Link](https://leetcode.com/problems/ambiguous-coordinates){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> ambiguousCoordinates(String s) {
    List<String> result = new ArrayList<>();
    int length = s.length();
    for (int idx = 1; idx < length - 2; idx++) {
      List<String> left = this.makeCoordinates(s.substring(1, idx + 1));
      List<String> right = this.makeCoordinates(s.substring(idx + 1, length - 1));
      for (String x : left) {
        for (String y : right) {
          result.add("(" + x + ", " + y + ")");
        }
      }
    }
    return result;
  }

  private List<String> makeCoordinates(String s) {
    List<String> list = new ArrayList<>();
    for (int idx = 1; idx <= s.length(); idx++) {
      String left = s.substring(0, idx);
      String right = s.substring(idx);
      if ((left.length() > 1 && left.charAt(0) == '0') || (right.length() > 0 && right.charAt(right.length() - 1) == '0')) {
        continue;
      }
      if (right.isEmpty()) {
        list.add(left);
      } else {
        list.add(left + "." + right);
      }
    }
    return list;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/ambiguous-coordinates/submissions/884958579/){:target="_blank"}

# 설명
1. s의 소괄호 내 숫자를 이용하여 x와 y축의 2차원 좌표를 만들 수 있는대로 모두 만드는 문제이다.
- s의 첫 문자와 마지막 문자는 소괄호의 시작 문자('(')와 종료 문자(')')이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과의 모든 좌표를 넣을 변수로, ArrayList로 초기화한다.
- length는 s의 길이를 저장한 변수이다.

3. 1부터 $length - 2$까지 idx를 증가시키며 아래를 수행한다.
- left에 s의 1부터 $idx + 1$자리까지 문자열을 잘라 4번의 makeCoordinates(String s) 메서드를 수행한 결과를 넣어준다.
- right에 left 이후의 s의 $idx + 1$부터 $length - 1$자리까지 문자열을 잘라 4번의 makeCoordinates(String s) 메서드를 수행한 결과를 넣어준다.
- x와 y를 이용하여 "(x, y)" 형태의 문자열로 result에 넣어준다.

4. 소수점인 좌표를 만들어줄 makeCoordinates(String s) 메서드를 정의한다.
- list는 만들 수 있는 좌표를 모두 만들어줄 변수로, ArrayList로 초기화한다.
- 1부터 s의 길이 이하까지 idx를 반복하며 아래를 수행한다.
  - left에 s의 처음부터 idx번째 문자까지 문자열을, right에 나머지 문자열을 넣어준다.
  - left의 길이가 1 초과이면서 첫 자리가 '0'이거나 right의 길이가 0 초과이면서 마지막 문자가 '0'인 경우 좌표를 생성하지 못하므로, 다음 반복을 수행한다.
  - right가 비어있는 경우, 정수 부분인 left만 list에 넣어준다.
  - right가 비어있지 않은 경우, 정수 부분인 left와 소수 부분인 right를 소수점('.')으로 구분하여 list에 넣어준다.
- 반복이 완료되면 list를 반환한다.

5. 3번의 반복이 완료되면 모든 좌표를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AmbiguousCoordinates.java){:target="_blank"}에서 확인 가능합니다.