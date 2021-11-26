---
title: "Leetcode Java Integer to English Words"
excerpt: "Leetcode Integer to English Words Java 풀이"
last_modified_at: 2021-11-26T09:00:00
header:
  image: /assets/images/leetcode/integer-to-english-words.png
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
[Link](https://leetcode.com/problems/integer-to-english-words/){:target="_blank"}

# 코드
```java
class Solution {

  private static String[] LOWER_THAN_20_WORDS = { "Zero", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine", "Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen" };
  private static String[] TEN_WORDS = { "", "", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety" };

  public String numberToWords(int num) {
    if (num == 0) {
      return "Zero";
    }
    int hundreds = num % 1000;
    num /= 1000;
    int thousands = num % 1000;
    num /= 1000;
    int millions = num % 1000;
    num /= 1000;
    int billions = num;
    StringBuilder sb = new StringBuilder();
    if (billions > 0) {
      this.hundredsToWord(billions, sb);
      this.addSpace(sb);
      sb.append("Billion ");
    }
    if (millions > 0) {
      this.hundredsToWord(millions, sb);
      this.addSpace(sb);
      sb.append("Million ");
    }
    if (thousands > 0) {
      this.hundredsToWord(thousands, sb);
      this.addSpace(sb);
      sb.append("Thousand ");
    }
    if (hundreds > 0) {
      this.hundredsToWord(hundreds, sb);
    }
    return sb.toString().trim();
  }

  private void addSpace(StringBuilder sb) {
    if (sb.length() - 1 != sb.lastIndexOf(" ")) {
      sb.append(" ");
    }
  }

  private void hundredsToWord(int num, StringBuilder sb) {
    int tens = num % 100;
    num /= 100;
    if (num > 0) {
      this.tensToWord(num, sb);
      sb.append(" Hundred ");
    }
    if (tens > 0) {
      this.tensToWord(tens, sb);
    }
  }

  private void tensToWord(int num, StringBuilder sb) {
    if (num < 20) {
      sb.append(LOWER_THAN_20_WORDS[num]);
    } else {
      int tens = num / 10;
      if (tens > 0) {
        sb.append(TEN_WORDS[tens]).append(" ");
      }
      num %= 10;
      if (num > 0) {
        sb.append(LOWER_THAN_20_WORDS[num]);
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/592694764/){:target="_blank"}

# 설명
1. 주어진 정수 num을 영문자열로 변환하는 문제이다.

2. 주어진 num이 0인 경우, "Zero"를 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 전역 변수를 정의한다.
- LOWER_THAN_20_WORDS은 20 미만의 숫자들을 영문자로 변경한 배열이다.
- TEN_WORDS는 10단위 숫자들을 영문자로 변경한 배열이다.
  - 단, 20 미만의 영문자에 10이 포함되기 때문에 10 자리에는 ""으로 두었다.

4. 문제 풀이에 필요한 10 단위를 영문자열로 변환하기 위한 tensToWord 메서드를 정의한다.
- num이 20 미만인 경우, LOWER_THAN_20_WORDS[num]의 영문자를 sb에 이어준다.
- num이 20 이상인 경우, 아래의 순서대로 진행한다.
  - tens에 nums을 10으로 나눈 몫을 넣어 tens가 0 보다 큰 경우, TEN_WORDS[tens]의 영문자를 sb에 이어준다.
  - num에 10으로 나눈 나머지 값을 넣고, num이 0 보다 큰 경우, LOWER_THAN_20_WORDS[num]의 영문자를 sb에 이어준다.

5. 문제 풀이에 필요한 100 단위를 영문자열로 변환하기 위한 hundredsToWord 메서드를 정의한다.
- tens에 num을 100으로 나눈 나머지 값을 넣어주고, num에 100으로 나눈 몫을 넣어준다.
- num이 0 보다 큰 경우, num의 값으로 tensToWord 메서드를 수행하여 sb에 hundred 단위의 영문자를 이어준 후 " Hundred " 문자열을 이어준다.
- tens가 0 보다 큰 경우, tensToWord에 tens를 이용하여 sb에 10단위의 영문자를 이어준다.

6. 문제 풀이에 필요한 sb의 앞 문자열에 " "이 들어간 경우에 대한 예외 처리를 공통화 하기 위한 addSpace 메서드를 정의한다.
- 만일 sb의 마지막 위치인 $sb.length() - 1$에 공백(" ")이 위치하지 않은 경우, 영문자열의 띄어쓰기 구분을 위해 sb에 공백(" ")을 넣어준다.

7. 문제 풀이에 필요한 변수를 정의한다.
- hundres, thousands, millions, billions에 차례대로 num을 1000으로 나눈 나머지 값을 넣어주고, num에 1000으로 나눈 몫을 넣어준다.
- 주어진 정수 num을 영문자열로 저장하기 위해 StringBuilder인 sb를 정의한다.
  - 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

8. billions가 0 보다 큰 경우 아래를 수행하여 billion 단위의 영문자를 완성한다.
- billions의 값으로 hundredsToWord 메서드를 수행하여 sb에 billion 단위의 영문자를 이어준다.
- addSpace 메서드를 수행하여 문자열 간 띄어쓰기 규칙을 유지한다.
- sb에 "Billion " 문자열을 이어주어 billion 단위의 영문자를 완성한다.

9. millions가 0 보다 큰 경우 아래를 수행하여 million 단위의 영문자를 완성한다.
- millions의 값으로 hundredsToWord 메서드를 수행하여 sb에 million 단위의 영문자를 이어준다.
- addSpace 메서드를 수행하여 문자열 간 띄어쓰기 규칙을 유지한다.
- sb에 "Million " 문자열을 이어주어 million 단위의 영문자를 완성한다.

10. thousands가 0 보다 큰 경우 아래를 수행하여 thousand 단위의 영문자를 완성한다.
- thousands의 값으로 hundredsToWord 메서드를 수행하여 sb에 thousand 단위의 영문자를 이어준다.
- addSpace 메서드를 수행하여 문자열 간 띄어쓰기 규칙을 유지한다.
- sb에 "Thousand " 문자열을 이어주어 thousand 단위의 영문자를 완성한다.

11. hundreds가 0 보다 큰 경우 아래를 수행하여 hundred 단위의 영문자를 완성한다.
- hundreds의 값으로 hundredsToWord 메서드를 수행하여 sb에 hundred 단위의 영문자를 이어준다.
- addSpace 메서드를 수행하여 문자열 간 띄어쓰기 규칙을 유지한다.
- sb에 "Hundred " 문자열을 이어주어 hundred 단위의 영문자를 완성한다.

12. 8 ~ 11로 영문자열이 저장된 sb를 문자열로 전환 후 앞,뒤 공백을 제거하고 주어진 문제로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IntegerToEnglishWords.java){:target="_blank"}에서 확인 가능합니다.