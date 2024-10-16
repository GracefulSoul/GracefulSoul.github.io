---
title: "Leetcode Java Valid Palindrome"
excerpt: "Leetcode Valid Palindrome Java 풀이"
last_modified_at: 2021-08-15T20:00:00
header:
  image: /assets/images/leetcode/valid-palindrome.png
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
[Link](https://leetcode.com/problems/valid-palindrome/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isPalindrome(String s) {
    char[] charArr = s.toCharArray();
    for (int i = 0, j = charArr.length - 1; i < j;) {
      if (!Character.isLetterOrDigit(charArr[i])) {
        i++;
      } else if (!Character.isLetterOrDigit(charArr[j])) {
        j--;
      } else if (Character.toLowerCase(charArr[i++]) != Character.toLowerCase(charArr[j--])) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/538837041/){:target="_blank"}

# 설명
1. 주어진 문자열 s가 영숫자 문자열만 포함하여 앞뒤로 읽어도 같은 문자열(이하 회문)이 되는지를 검증하는 문제이다.

2. 주어진 문자열 s를 문자의 배열로 변환하여 변수 charArr를 정의한다.

3. 반복을 통해서 i는 처음부터, j는 뒤에서부터 i가 j보다 작을 때 까지 반복한다.
- 만일 charArr[i]가 문자나 숫자가 아닌 경우 무시해야 하므로, i를 증가시킨다.
- 만일 charArr[j]가 문자나 숫자가 아닌 경우 무시해야 하므로, j를 감소시킨다.
- 그 외의 경우 charArr[i]와 charArr[j]가 같지 않으면 회문이 되지 못하므로, false를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 해당 문자열이 회문이므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidPalindrome.java){:target="_blank"}에서 확인 가능합니다.