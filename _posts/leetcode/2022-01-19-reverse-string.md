---
title: "Leetcode Java Reverse String"
excerpt: "Leetcode Reverse String Java 풀이"
last_modified_at: 2022-01-19T13:00:00
header:
  image: /assets/images/leetcode/reverse-string.png
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
[Link](https://leetcode.com/problems/reverse-string/){:target="_blank"}

# 코드
```java
class Solution {

  public void reverseString(char[] s) {
    int left = 0;
    int right = s.length - 1;
    while (left < right) {
      char temp = s[left];
      s[left] = s[right];
      s[right] = temp;
      left++;
      right--;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/622947023/){:target="_blank"}

# 설명
1. 주어진 문자 배열 s를 반전시키는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- left는 좌측의 값을 반전시키기 위한 인덱스로, 0으로 초기화한다.
- right는 우측의 값을 반전시키기 위한 인덱스로, $s.length - 1$의 값으로 초기화한다.

3. left가 right보다 작을 때 까지 반복하여 배열을 반전시킨다.
- temp에 s의 left번째 문자를 넣고, s의 left번째 자리에 s의 right번째 문자를 넣어준다.
- s의 right번째 문자를 넣어주고, s의 right번째 자리에 temp를 넣어 문자의 위치를 바꾸어 준다.
- left를 증가시키고, right를 감소시키며 반복을 계속 수행하여 모든 문자의 위치를 바꾸어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReverseString.java){:target="_blank"}에서 확인 가능합니다.