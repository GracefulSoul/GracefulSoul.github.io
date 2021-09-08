---
title: "Leetcode Java Reverse Words in a String"
excerpt: "Leetcode Reverse Words in a String Java 풀이"
last_modified_at: 2021-09-08T13:00:00
header:
  image: /assets/images/leetcode/reverse-words-in-a-string.png
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
[Link](https://leetcode.com/problems/reverse-words-in-a-string/){:target="_blank"}

# 코드
```java
class Solution {

  public String reverseWords(String s) {
    char[] charArr = s.toCharArray();
    int length = charArr.length;
    this.reverse(charArr, 0, length - 1);
    this.reverseWords(charArr, length);
    return this.cleanSpaces(charArr, length);
  }

  private void reverse(char[] charArr, int i, int j) {
    while (i < j) {
      char temp = charArr[i];
      charArr[i++] = charArr[j];
      charArr[j--] = temp;
    }
  }

  private void reverseWords(char[] charArr, int length) {
    int i = 0;
    int j = 0;
    while (i < length) {
      while (i < j || i < length && charArr[i] == ' ') {
        i++;
      }
      while (j < i || j < length && charArr[j] != ' ') {
        j++;
      }
      this.reverse(charArr, i, j - 1);
    }
  }

  private String cleanSpaces(char[] charArr, int length) {
    int i = 0;
    int j = 0;
    while (j < length) {
      while (j < length && charArr[j] == ' ') {
        j++;
      }
      while (j < length && charArr[j] != ' ') {
        charArr[i++] = charArr[j++];
      }
      while (j < length && charArr[j] == ' ') {
        j++;
      }
      if (j < length) {
        charArr[i++] = ' ';
      }
    }
    return new String(charArr).substring(0, i);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/551262482/){:target="_blank"}

# 설명
1. 주어진 문자열 s의 단어들의 순서를 반전시키는 문제이다.
- 단 주어진 문자열 s에서 복수개 공백을 사용한 경우, 하나의 공백으로 변환해야 한다.
- 또한 주어진 문자열 s의 앞과 뒤에 포함된 공백은 제거해야 한다.

2. 문제 풀이에 필요한 변수들을 정의한다.
- charArr은 s를 문자 배열로 만들어 반전시키기 위해 정의한다.
- length는 charArr의 길이를 저장할 변수이다.

3. charArr의 모든 문자를 반전시킨다.

4. 공백(' ')으로 구분하여 문자열을 반전시켜 원래의 단어로 복원시킨다.
- 문제 풀이에 필요한 변수들을 정의한다.
  - i는 단어의 시작 index를 저장하기 위한 변수이다.
  - j는 단어의 종료 index를 저장하기 위한 변수이다.
- 단어를 찾는 기본 원칙은 공백(' ')을 구분하여 단어를 찾아 i와 j를 정의한다.
- 3번에서 사용한 방식으로 i부터 $j - 1$까지 문자를 반전시켜 해당 문자열을 원래의 단어로 복원시킨다.

5. 문제의 세부 요건인 공백('')에 대한 부분을 제거하기 위해 모든 문자열을 탐색하여 조건을 충족시킨 문자열로 변환하여 주어진 문제의 결과로 반환한다.
- 문제 풀이에 필요한 변수들을 정의한다.
  - i는 세부 요건을 충족한 문자열을 완성하기 위한 index로 사용하는 변수이다.
  - j는 전체 문자열을 탐색하기 위한 index이다.
- charArr의 전체 문자들을 반복하여 세부 요건들을 충족시킨다.
  - j가 length보다 작고 charArr[j]가 공백(' ')일 경우, j를 증가시켜 단어의 시작 위치를 찾는다.
  - j가 length보다 작고 charArr[j]가 공백(' ')이 아닐 경우, charArr[i]에 charArr[j]를 넣어 순차적인 문장을 만들어주고 i와 j를 증가시킨다.
  - j가 length보다 작고 charArr[j]가 공백(' ')일 경우, j를 증가시켜 다음 단어의 시작 위치를 찾는다.
  - 마지막 반복을 통해서 j가 length보다 작을 경우, charArr[i]에 공백(' ')을 넣어주고 i를 증가시켜준다.
- 반복이 완료되면 charArr를 새로운 문자열로 바꾸고, 문자열의 처음부터 i 번째 전까지 잘라 요구 사항을 충족하년 문자열로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EvaluateReversePolishNotation.java){:target="_blank"}에서 확인 가능합니다.