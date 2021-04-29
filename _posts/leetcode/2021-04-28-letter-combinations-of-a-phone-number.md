---
title: "Leetcode Java Letter Combinations of a Phone Number"
excerpt: "Leetcode Letter Combinations of a Phone Number Java 풀이"
last_modified_at: 2021-04-28T12:40:00
header:
  image: /assets/images/leetcode/letter-combinations-of-a-phone-number.png
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
[Link](https://leetcode.com/problems/letter-combinations-of-a-phone-number/){:target="_blank"}

# 코드
```java
class Solution {

  private static final String[] MAPPING = new String[] { "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz" };

  public List<String> letterCombinations(String digits) {
    List<String> result = new LinkedList<String>();
    if (!digits.isEmpty()) {
      this.combination("", digits, result);
    }
    return result;
  }

  private void combination(String prefix, String digits, List<String> result) {
    if (prefix.length() == digits.length()) {
      result.add(prefix);
      return;
    }
    String letters = MAPPING[(digits.charAt(prefix.length()) - '0')];
    for (int i = 0; i < letters.length(); i++) {
      this.combination(this.addCharToString(prefix, letters.charAt(i)), digits, result);
    }
  }

  private String addCharToString(String s, Character c) {
    StringBuilder sb = new StringBuilder(s);
    sb.append(c);
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/485817328/){:target="_blank"}

# 설명
1. 각 다이얼 숫자가 가진 문자들을 mapping 변수에 정의한다.
  - 재귀호출로 재활용되는 변수이므로, 전역 변수로 지정한다.

2. 각 다이얼 숫자가 가진 문자들의 복합 문자열을 저장하기 위한 변수 result를 선언한다.
  - 순서에 맞추어 저장하기 위해서 [LinkedList](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html){:target="_blank"}를 사용한다.

3. 만일 주어진 정수열 digits의 길이가 0인 경우, 문자의 조합이 의미가 없으므로 문제의 결과로 빈 Collection인 result를 주어진 문제의 결과로 반환한다.

4. 재귀 함수를 사용하여 주어진 문자열을 기반으로 결과를 변수 result에 저장하고 해당 재귀를 종료한다.
  - 만일 주어진 문자열 digits의 길이와 결과의 문자열 길이인 prefix의 길이가 같거나 크다면 해당 문자열은 주어진 문제의 결과 중 하나이다.

5. 주어진 문자열의 특정 자릿수의 다이얼 문자들을 letter에 임시 저장한다.
  - 기존 문제들과 유사하게 특정 자릿수의 index를 가져오는 방법은 character 형의 숫자 문자를 '0'으로 빼주게 되면 Ascii code 10진수 기반으로 자기 자신의 숫자로 반환된다.

6. 특정 자릿수의 다이얼 문자들을 한 자리씩 prefix에 덧붙이고 재귀 호출을 반복한다.
  - 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.
  - 위의 4번의 조건에 의해 재귀 호출은 각각 마무리되고 결과를 변수 result에 저장하게된다.

7. 반복이 끝나면 각 다이얼 숫자가 가진 문자들의 복합 문자열을 저장한 변수 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LetterCombinationsOfAPhoneNumber.java){:target="_blank"}에서 확인 가능합니다.