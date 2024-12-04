---
title: "Leetcode Java Make String a Subsequence Using Cyclic Increments"
excerpt: "Leetcode - 'Make String a Subsequence Using Cyclic Increments' 문제 Java 풀이"
last_modified_at: 2024-12-04T18:50:00
header:
  image: /assets/images/leetcode/make-string-a-subsequence-using-cyclic-increments.png
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
[Link](https://leetcode.com/problems/make-string-a-subsequence-using-cyclic-increments/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canMakeSubsequence(String str1, String str2) {
    int i = 0;
    int length = str2.length();
    for (char c : str1.toCharArray()) {
      if (i < length && (str2.charAt(i) - c + 26) % 26 <= 1) {
        i++;
      }
    }
    return i == length;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/make-string-a-subsequence-using-cyclic-increments/submissions/1470033738/){:target="_blank"}

# 설명
1. 영소문자로 이루어진 str1의 각 문자를 아래의 규칙으로 변경하여 str2가 부분 문자열로 포함되는지 검증하는 문제이다.
- str1의 임의 위치인 i번째 문자인 str1[i]를 앞뒤 문자 중 하나로 변경 가능하다.
- a 다음 문자는 b, z 다음 문자는 a가 되는 a ~ z까지 문자들이 계속 반복된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- i는 str2의 위치를 저장할 변수로, 0으로 초기화한다.
- length는 str2의 길이를 저장한 변수이다.

3. st1의 각 문자들을 c에 순차적으로 넣고 아래를 수행한다.
- i가 length 미만이면서 str의 i번째 문자에 c를 뺀 문자의 차잇값이 1 이하일 때, i를 증가시킨다.

4. i가 length와 동일한 부분 배열이 가능한지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MakeStringASubsequenceUsingCyclicIncrements.java){:target="_blank"}에서 확인 가능합니다.