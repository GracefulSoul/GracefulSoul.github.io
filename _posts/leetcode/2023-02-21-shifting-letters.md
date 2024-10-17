---
title: "Leetcode Java Shifting Letters"
excerpt: "Leetcode - 'Shifting Letters' 문제 Java 풀이"
last_modified_at: 2023-02-21T20:20:00
header:
  image: /assets/images/leetcode/shifting-letters.png
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
[Link](https://leetcode.com/problems/shifting-letters){:target="_blank"}

# 코드
```java
class Solution {

  public String shiftingLetters(String s, int[] shifts) {
    char[] charArray = s.toCharArray();
    int shift = 0;
    for (int i = s.length() - 1; i >= 0; i--) {
      shift += shifts[i] % 26;
      charArray[i] = (char) (((charArray[i] - 'a') + shift) % 26 + 'a');
    }
    return new String(charArray);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/shifting-letters/submissions/902200498/){:target="_blank"}

# 설명
1. 문자열 s의 각 위치 별 문자를 shifts의 위치 별 숫자의 누계까지 영문자 기준으로 우측으로 이동하는 문제이다.
- 'a'를 우측으로 한 칸 이동하면 'b'가 되고, 'z'를 우측으로 한 칸 이동하면 'a'가 된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자별로 나눈 배열로 저장한 변수이다.
- shift는 shifts를 이동하며 각 문자의 이동 횟수를 저장할 변수로, 0으로 초기화한다.

3. s의 마지막 위치에서 0까지 i를 감소시키며 우측에서 좌측으로 이동하며 아래를 계산한다.
- shift에 shifts의 i번째 값을 영문자의 개수인 26으로 나눈 나머지 값을 더해준다.
- charArray의 i번째 위치에 charArray의 i번째 문자를 우측으로 shift번 이동하고 26으로 나눈 나머지 값에 해당하는 위치의 영문자로 넣어준다.

4. 반복이 완료되면 charArray를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShiftingLetters.java){:target="_blank"}에서 확인 가능합니다.