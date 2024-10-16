---
title: "Leetcode Java Reverse Only Letters"
excerpt: "Leetcode Reverse Only Letters Java"
last_modified_at: 2023-05-06T09:00:00
header:
  image: /assets/images/leetcode/reverse-only-letters.png
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
[Link](https://leetcode.com/problems/reverse-only-letters){:target="_blank"}

# 코드
```java
class Solution {

  public String reverseOnlyLetters(String s) {
    char[] charArray = s.toCharArray();
    int left = 0;
    int right = charArray.length - 1;
    while (left < right) {
      if (!Character.isAlphabetic(charArray[left])) {
        left++;
      } else if (!Character.isAlphabetic(charArray[right])) {
        right--;
      } else {
        char temp = charArray[left];
        charArray[left++] = charArray[right];
        charArray[right--] = temp;
      }
    }
    return new String(charArray);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reverse-only-letters/submissions/945218187/){:target="_blank"}

# 설명
1. 문자열 s의 영문자만 앞뒤 순서를 변경하는 문제이다.
- 영문자가 아닌 다른 문자들은 위치를 그대로 유지해야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- left와 right는 문자열의 좌측과 우측의 위치 변수로, 0과 $charArray.length - 1$로 초기화한다.

3. left가 right보다 작을 때 까지 아래를 반복한다.
- charArray의 left번째 문자가 알파벳이 아닌 경우, left를 증가시켜 다음 위치로 이동시킨다.
- charArray의 right번째 문자가 알파벳이 아닌 경우, right를 감소시켜 다음 위치로 이동시킨다.
- 둘 다 알파벳인 경우, charArray의 left번째 문자와 right번째 문자를 교환한다.

4. 반복이 완료되면 charArray를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseOnlyLetters.java){:target="_blank"}에서 확인 가능합니다.