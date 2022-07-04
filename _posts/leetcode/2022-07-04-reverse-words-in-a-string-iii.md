---
title: "Leetcode Java Reverse Words in a String III"
excerpt: "Leetcode Reverse Words in a String III Java"
last_modified_at: 2022-07-04T19:30:00
header:
  image: /assets/images/leetcode/reverse-words-in-a-string-iii.png
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
[Link](https://leetcode.com/problems/reverse-words-in-a-string-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public String reverseWords(String s) {
    char[] charArray = s.toCharArray();
    int start = 0;
    int end = 0;
    while (end < charArray.length) {
      if (charArray[end] == ' ') {
        this.reverse(charArray, start, end - 1);
        start = end + 1;
      }
      end++;
    }
    this.reverse(charArray, start, end - 1);
    return new String(charArray);
  }

  private void reverse(char[] charArray, int start, int end) {
    while (start < end) {
      char temp = charArray[start];
      charArray[start++] = charArray[end];
      charArray[end--] = temp;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/738136794/){:target="_blank"}

# 설명
1. s의 문장 순서 그대로 각 단어들을 반전시켜 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환하여 저장한 변수이다.
- start와 end는 문자를 반전시킬 시작과 종료 위치를 넣을 변수로, 0으로 초기화한다.

3. end가 charArray의 길이 미만일 때 까지 반복을 수행한다.
- charArray의 end번째 문자가 띄어쓰기(" ")인 경우, charArray의 start 부터 $end - 1$번째 문자까지 반전시키고 start에 $end + 1$을 넣어준다.
- end를 증가시키고 반복을 계속 수행한다.

4. 반복이 완료되면 마지막 단어인 charArray의 start부터 $end - 1$번째 문자까지 반전시키고 문자열로 전환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseWordsInAStringIII.java){:target="_blank"}에서 확인 가능합니다.