---
title: "Leetcode Java Minimum Window Substring"
excerpt: "Leetcode Minimum Window Substring Java 풀이"
last_modified_at: 2021-06-25T07:10:00
header:
  image: /assets/images/leetcode/minimum-window-substring.png
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
[Link](https://leetcode.com/problems/minimum-window-substring/){:target="_blank"}

# 코드
```java
class Solution {

  public String minWindow(String s, String t) {
    int[] charArray = new int[128];
    for (char c : t.toCharArray()) {
      charArray[c]++;
    }
    int start = 0;
    int length = Integer.MAX_VALUE;
    int counter = t.length();
    for (int i = 0, j = 0; i < s.length(); i++) {
      if (charArray[s.charAt(i)]-- > 0) {
        counter--;
      }
      while (counter == 0) {
        if (i - j + 1 < length) {
          length = i - j + 1;
          start = j;
        }
        if (++charArray[s.charAt(j++)] > 0) {
          counter++;
        }
      }
    }
    return length == Integer.MAX_VALUE ? "" : s.substring(start, start + length);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/512748176/){:target="_blank"}

# 설명
1. 주어진 문자열 s에 문자열 t의 문자들이 포함된 최소 부분 문자열을 구하는 문제이다.

2. 주어진 문자열 t의 문자 갯수를 저장하기 위한 배열 charArray를 선언하고, t의 각 문자열의 숫자만큼 해당 배열의 ASCII 코드 자리의 숫자를 증가시킨다.

3. 문제를 해결하기 위한 변수를 정의한다.
- 부분 문자열의 시작의 인덱스를 저장할 start 변수를 0으로 정의한다.
- 부분 문자열의 길이를 저장할 length 변수를 최대 정수 값인 Integer.MAX_VALUE로 저장한다.
- 문자열 t의 문자 갯수를 저장하는 counter 변수를 문자열 t의 길이로 정의한다.

4. 문자열 s의 길이만큼 반복하여 부분 문자열이 존재하는지를 확인하고, 존재 할 경우 부분 문자열의 시작과 문자열의 길이를 확인하여 start와 length 변수의 값으로 넣어준다.
- 배열 charArray 내 s의 i번째 자리 문자 ASCII 코드번째 값이 0보다 클 경우, 해당 값과 counter를 감소시킨다.
- 만일 counter의 값이 0일 경우, 주어진 문자열 t로 구성된 문자들이 문자열 s에 모두 포함되었으므로 부분 문자열을 구한다.
  - $i - j + 1$이 length보다 작을 경우, length의 값에 $i - j + 1$을 넣고, start의 값에 j를 넣어준다.
  - 배열 charArray 내 s의 j번째 자리 문자 ASCII 코드 값을 증가시키고, 해당 값이 0보다 클 경우 counter를 증가시킨다.

5. 반복이 완료되면 length가 변경되었는지를 확인하여 주어진 문제의 결과를 반환한다.
- length의 값이 그대로 Integer.MAX_VALUE인 경우, 매칭된 부분 문자열이 없으므로 빈 문자열인 ""을 주어진 문제의 결과로 반환한다.
- length의 값이 변경되었으면, 매칭된 부분 문자열이 존재하므로 주어진 문자열 s의 start 인덱스부터 $start + length$번째 문자열까지 잘라 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumWindowSubstring.java){:target="_blank"}에서 확인 가능합니다.