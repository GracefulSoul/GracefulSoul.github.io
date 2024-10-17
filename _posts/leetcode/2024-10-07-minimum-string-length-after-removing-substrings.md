---
title: "Leetcode Minimum String Length After Removing Substrings"
excerpt: "Leetcode Easy - 'Minimum String Length After Removing Substrings' 문제 Java 풀이"
last_modified_at: 2024-10-07T18:30:00
header:
  image: /assets/images/leetcode/minimum-string-length-after-removing-substrings.png
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
[Link](https://leetcode.com/problems/minimum-string-length-after-removing-substrings/){:target="_blank"}

# 코드
```java
class Solution {

  public int minLength(String s) {
    Stack<Character> stack = new Stack<>();
    for (char c : s.toCharArray()) {
      if (!stack.isEmpty() && ((c == 'B' && stack.peek() == 'A') || (c == 'D' && stack.peek() == 'C'))) {
        stack.pop();
      } else {
        stack.push(c);
      }
    }
    return stack.size();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-string-length-after-removing-substrings/submissions/1414594298/){:target="_blank"}

# 설명
1. 영문 대문자로 이루어진 s에서 "AB"와 "CD"를 계속 제거하고 남은 문자열의 길이를 구하는 문제이다.

2. stack은 s의 문자들을 순차적으로 넣었다가 뺄 변수로, Stack으로 초기화한다.

3. s의 문자를 순차적으로 c에 넣어 아래를 반복한다.
- stack이 비어있지 않으면서 아래 두 조건 중 하나라도 만족하는 경우, stack에서 마지막 문자를 제거한다.
  - c가 'B' 문자이면서 stack의 마지막 문자가 'A'인 "AB" 문자열인 경우.
  - c가 'D' 문자이면서 stack의 마지막 문자가 'C'인 "CD" 문자열인 경우.
- 위의 경우가 아니라면, stack에 c를 넣어준다.

4. 반복이 완료되면 남은 문자열의 길이인 stack의 길이를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumStringLengthAfterRemovingSubstrings.java){:target="_blank"}에서 확인 가능합니다.