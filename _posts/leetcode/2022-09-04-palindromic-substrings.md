---
title: "Leetcode Java Palindromic Substrings"
excerpt: "Leetcode - 'Palindromic Substrings' 문제 Java 풀이"
last_modified_at: 2022-09-04T09:00:00
header:
  image: /assets/images/leetcode/palindromic-substrings.png
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
[Link](https://leetcode.com/problems/palindromic-substrings/){:target="_blank"}

# 코드
```java
class Solution {

  public int countSubstrings(String s) {
    int count = 0;
    char[] charArray = s.toCharArray();
    for (int idx = 0; idx < s.length(); idx++) {
      count += this.isPalindrome(charArray, idx, idx) + this.isPalindrome(charArray, idx, idx + 1);
    }
    return count;
  }

  private int isPalindrome(char[] charArray, int start, int end) {
    int count = 0;
    while (start >= 0 && end < charArray.length && charArray[start] == charArray[end]) {
      count++;
      start--;
      end++;
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/790848726/){:target="_blank"}

# 설명
1. 문자열 s 내 앞뒤로 읽어도 같은 문자열(이하 회문)을 만들 수 있는 하위 문자열의 수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 문제에 해당하는 하위 문자열의 수를 계산하기 위한 변수로, 0으로 초기화한다.
- charArray는 문자열 s를 문자 배열로 저장하기 위한 변수이다.

3. 0부터 s의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- count에 4번에서 정의한 isPalindrome(char[] charArray, int start, int end) 메서드를 end에 idx와 $idx + 1$인 홀수와 짝수의 경우를 각각 계산하여 더해준다.

4. 회문이 되는 문자열의 수를 계산하기 위한 isPalindrome(char[] charArray, int start, int end)을 정의한다.
- count는 start부터 end까지 회문이 되는 문자열의 숫자로, 0으로 초기화한다.
- start가 0 이상이고, end가 charArray 길이 미만이면서 charArray의 start번째 문자와 end번째 문자가 동일하면 아래를 수행한다.
  - 위를 만족하면 회문이 되므로, count를 증가시킨다.
  - 범위를 축소하기 위해 start를 감소시키고, end를 증가시킨다.
- 반복이 완료되면 count를 반환한다.

5. 모든 수행이 완료되면 회문을 만들 수 있는 하위 문자열의 수를 계산한 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PalindromicSubstrings.java){:target="_blank"}에서 확인 가능합니다.