---
title: "Leetcode Java Check if One String Swap Can Make Strings Equal"
excerpt: "Leetcode - 'Check if One String Swap Can Make Strings Equal' 문제 Java 풀이"
last_modified_at: 2025-02-05T19:30:00
header:
  image: /assets/images/leetcode/check-if-one-string-swap-can-make-strings-equal.png
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
[Link](https://leetcode.com/problems/check-if-one-string-swap-can-make-strings-equal/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean areAlmostEqual(String s1, String s2) {
    char[] s1CharArray = s1.toCharArray();
    char[] s2CharArray = s2.toCharArray();
    int i = -1;
    int j = -1;
    int count = 0;
    for (int k = 0; k < s1CharArray.length; k++) {
      if (s1CharArray[k] != s2CharArray[k]) {
        count++;
        if (i == -1) {
          i = k;
        } else if (j == -1) {
          j = k;
        }
      }
    }
    return count == 0 || (count == 2 && s1CharArray[i] == s2CharArray[j] && s1CharArray[j] == s2CharArray[i]);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-one-string-swap-can-make-strings-equal/submissions/1532178071/){:target="_blank"}

# 설명
1. 문자열 s1에서 문자들 간 스왑을 최대 한 번만 사용하여 s2를 만들 수 있는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- s1CharArray와 s2CharArray는 s1과 s2를 문자 배열로 변환한 변수이다.
- i와 j는 문자 스왑을 위한 위치 변수로, 둘 다 -1로 초기화한다.
- count는 s1과 s2의 다른 문자 갯수를 계산하기 위한 변수로, 0으로 초기화한다.

3. 0부터 s1CharArray의 길이 미만까지 k를 증가시키며 아래를 반복한다.
- s1CharArray[k] 문자와 s2CharArray[k] 문자가 다른 경우, 아래를 수행한다.
  - count를 증가시켜 다른 갯수를 계산한다.
  - i가 -1이면 i에 k를, j가 -1이면 j에 k를 넣어 스왑할 위치를 저장한다.

4. 반복이 완료되면 아래의 두 경우 중 하나라도 만족하면 true를, 아니면 false를 주어진 문제의 결과로 반환한다.
- count가 0인 스왑할 대상이 없는 경우.
- count가 2이면서, s1CharArray[i] 문자와 s2CharArray[j] 문자가 같으면서 s1CharArray[j] 문자와 s2CharArray[i] 문자가 동일한 스왑하면 동일한 문자열이 되는 경우.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfOneStringSwapCanMakeStringsEqual.java){:target="_blank"}에서 확인 가능합니다.