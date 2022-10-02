---
title: "Leetcode Java Valid Palindrome II"
excerpt: "Leetcode Valid Palindrome II Java"
last_modified_at: 2022-10-03T08:30:00
header:
  image: /assets/images/leetcode/valid-palindrome-ii.png
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
[Link](https://leetcode.com/problems/valid-palindrome-ii){:target="_blank"}

# 코드
```java
class Solution {

  public boolean validPalindrome(String s) {
    char[] charArray = s.toCharArray();
    int length = s.length();
    int index = this.isPalindrome(charArray, 0, length - 1);
    if (index == -1) {
      return true;
    } else {
      return this.isPalindrome(charArray, index + 1, length - index - 1) == -1
          || this.isPalindrome(charArray, index, length - index - 2) == -1;
    }
  }

  private int isPalindrome(char[] charArray, int left, int right) {
    while (left < right) {
      if (charArray[left] != charArray[right]) {
        return left;
      }
      left++;
      right--;
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/813821139/){:target="_blank"}

# 설명
1. 문자열 s에서 최대 하나의 문자를 제거하여 앞뒤로 같은 문자열(이하 회문)이 되는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환해서 저장한 변수이다.
- length는 s의 길이를 저장한 변수이다.
- index는 3번을 통해 s의 처음부터 끝까지 회문이 되는 지점을 검증한 값을 탐색하여 넣어준다.

3. 회문이 되는 지점을 탐색하기 위한 isPalindrome(char[] charArray, int left, int right) 메서드를 정의한다.
- left가 right보다 작을 때 까지 아래를 반복한다.
  - charArray의 left번째 문자와 right번째 문자가 다른 경우 회문이 틀어지는 위치이므로, left를 반환한다.
  - 위의 경우가 아니라면 left를 증가시키고 right를 감소시켜 검증 범위를 좁혀주고 반복을 계속 수행한다.
- 반복이 완료되면 정상적으로 회문이 되는 경우이므로, -1을 반환한다.

4. index가 -1인 경우 s가 정상적으로 회문이 되므로, true를 주어진 문제의 결과로 반환한다.

5. index가 -1보다 큰 경우 아래의 경우대로 index번쨰 문자나 마지막 문자를 제거하고 검증하여 하나라도 만족하면 true를, 둘 다 만족하지 않으면 false를 주어진 문제의 결과로 반환한다.
- index의 문자를 제외하는 $index + 1$ 부터 $length - index - 1$ 까지 isPalindrome(char[] charArray, int left, int right) 메서드를 수행한 값이 -1인지 검증한 결과.
- 마지막 문자를 제외하는 index 부터 $length - index - 2$ 까지 isPalindrome(char[] charArray, int left, int right) 메서드를 수행한 값이 -1인지 검증한 결과.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidPalindromeII.java){:target="_blank"}에서 확인 가능합니다.