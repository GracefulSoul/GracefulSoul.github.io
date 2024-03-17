---
title: "Leetcode Java Remove All Adjacent Duplicates In String"
excerpt: "Leetcode Remove All Adjacent Duplicates In String Java"
last_modified_at: 2024-03-17T12:20:00
header:
  image: /assets/images/leetcode/remove-all-adjacent-duplicates-in-string.png
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
[Link](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string){:target="_blank"}

# 코드
```java
class Solution {

  public String removeDuplicates(String s) {
    StringBuilder sb = new StringBuilder();
    for (char c : s.toCharArray()) {
      if (sb.length() > 0 && sb.charAt(sb.length() - 1) == c) {
        sb.deleteCharAt(sb.length() - 1);
      } else {
        sb.append(c);
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/submissions/1205892792/){:target="_blank"}

# 설명
1. 문자열 s에서 인접한 동일 문자들을 반복 제거한 문자열을 반환하는 문제이다.

2. sb는 동적으로 문자열을 이어주기 위한 변수로, StringBuilder로 초기화한다.

3. s의 문자들을 순차적으로 c 에 넣어 아래를 반복한다.
- sb의 길이가 0보다 크면서 sb의 이전 문자가 c와 동일한 경우, sb의 이전 문자를 제거한다.
- 위의 경우가 아니라면 sb에 c를 이어준다.

4. 반복이 완료되면 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveAllAdjacentDuplicatesInString.java){:target="_blank"}에서 확인 가능합니다.