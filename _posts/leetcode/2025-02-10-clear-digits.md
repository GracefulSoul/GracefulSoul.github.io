---
title: "Leetcode Java Clear Digits"
excerpt: "Leetcode - 'Clear Digits' 문제 Java 풀이"
last_modified_at: 2025-02-10T18:30:00
header:
  image: /assets/images/leetcode/clear-digits.png
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
[Link](https://leetcode.com/problems/clear-digits/){:target="_blank"}

# 코드
```java
class Solution {

  public String clearDigits(String s) {
    StringBuilder sb = new StringBuilder();
    for (char c : s.toCharArray()) {
      if (Character.isDigit(c)) {
        int length = sb.length();
        if (length > 0) {
          sb.deleteCharAt(length - 1);
        }
      } else {
        sb.append(c);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/design-a-number-container-system/submissions/1535362698/){:target="_blank"}

# 설명
1. 문자열 s에서 숫자가 존재하는 경우, 해당 값과 좌측 값을 같이 제거 후 동일한 절차를 반복하여 더 이상 제거할 문자가 없는 문자열을 반환하는 문제이다.

2. sb는 결과 문자열을 저장할 변수로, 동적 문자열 생성을 위해 StringBuilder로 초기화한다.

3. s의 각 문자들을 순차적으로 c에 넣어 아래를 수행한다.
- c가 숫자인 경우, sb에 문자가 추가된 경우 마지막 문자를 제거하여 반복 조건을 만족시킨다.
- c가 문자인 경우, sb 다음 문자로 이어 넣어준다.

4. 반복이 완료되면 완성된 sb를 문자열로 반환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ClearDigits.java){:target="_blank"}에서 확인 가능합니다.