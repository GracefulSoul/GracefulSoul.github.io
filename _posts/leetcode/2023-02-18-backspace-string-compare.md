---
title: "Leetcode Java Split Backspace String Compare"
excerpt: "Leetcode Split Backspace String Compare Java"
last_modified_at: 2023-02-18T09:00:00
header:
  image: /assets/images/leetcode/backspace-string-compare.png
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
[Link](https://leetcode.com/problems/backspace-string-compare){:target="_blank"}

# 코드
```java
class Solution {

  public boolean backspaceCompare(String s, String t) {
    int i = s.length() - 1;
    int j = t.length() - 1;
    int back = 0;
    while (true) {
      back = 0;
      while (i >= 0 && (back > 0 || s.charAt(i) == '#')) {
        back += s.charAt(i--) == '#' ? 1 : -1;
      }
      back = 0;
      while (j >= 0 && (back > 0 || t.charAt(j) == '#')) {
        back += t.charAt(j--) == '#' ? 1 : -1;
      }
      if (i >= 0 && j >= 0 && s.charAt(i) == t.charAt(j)) {
        i--;
        j--;
      } else {
        break;
      }
    }
    return i == -1 && j == -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/backspace-string-compare/submissions/900037562/){:target="_blank"}

# 설명
1. s와 t를 텍스트 편집기에 한 문자씩 입력할 때, 동일한 문자열이 되는지 검증하는 문제이다.
- '#' 문자는 백스페이스를 의미하며 앞의 문자를 제거한다.

2. i와 j는 s 문자와 t 문자의 위치를 마지막 위치를 저장한 변수이다.

3. 아래의 반복을 종료하기 전까지 계속 반복한다.
- back은 '#'의 갯수를 저장하기 위한 변수로, i와 j를 뒤에서부터 #이 존재하는 갯수만큼 앞의 문자를 차감하여 위치를 이동시킨다.
- i와 j가 0보다 크거나 같으면서 i와 j가 동일하면 i와 j를 감소시키고, 아니면 반복을 그만한다.

4. 검증된 문자열의 두 위치 변수인 i와 j가 -1인지 검증한 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BackspaceStringCompare.java){:target="_blank"}에서 확인 가능합니다.