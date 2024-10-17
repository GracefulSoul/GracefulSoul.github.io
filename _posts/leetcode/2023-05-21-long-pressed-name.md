---
title: "Leetcode Java Long Pressed Name"
excerpt: "Leetcode - 'Long Pressed Name' 문제 Java 풀이"
last_modified_at: 2023-05-21T13:40:00
header:
  image: /assets/images/leetcode/long-pressed-name.png
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
[Link](https://leetcode.com/problems/long-pressed-name){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isLongPressedName(String name, String typed) {
    int i = 0;
    int j = 0;
    while (j < typed.length()) {
      if (i < name.length() && name.charAt(i) == typed.charAt(j)) {
        i++;
      } else if (j == 0 || typed.charAt(j - 1) != typed.charAt(j)) {
        return false;
      }
      j++;
    }
    return i == name.length();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/long-pressed-name/submissions/954292072/){:target="_blank"}

# 설명
1. typed의 중복 문자를 제거하고 name이 될 수 있는지 검증하는 문제이다.

2. i와 j는 name과 typed를 검증하기 위한 위치 변수로, 둘 다 0으로 초기화한다.

3. j가 typed의 길이 미만일 때 까지 아래를 반복한다.
- i가 name의 길이 미만이면서 name의 i번째 문자와 typed의 j번째 문자가 동일한 경우, i를 증가시킨다.
- 위가 아니면서 j가 0이거나 typed의 $j - 1$번째 문자와 j번째 문자가 동일하지 않은 경우 name과 다른 값이 입력되었으므로, 주어진 문제의 결과로 false를 반환한다.
- j를 증가시키고 다음 반복을 계속 한다.

4. 반복이 완료되면 i가 nmae의 길이와 동일한지 검증한 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongPressedName.java){:target="_blank"}에서 확인 가능합니다.