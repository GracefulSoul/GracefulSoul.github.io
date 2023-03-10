---
title: "Leetcode Java Remove Duplicate Letters"
excerpt: "Leetcode Remove Duplicate Letters Java 풀이"
last_modified_at: 2021-12-26T15:00:00
header:
  image: /assets/images/leetcode/remove-duplicate-letters.png
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
[Link](https://leetcode.com/problems/remove-duplicate-letters/){:target="_blank"}

# 코드
```java
class Solution {

  public String removeDuplicateLetters(String s) {
    StringBuilder sb = new StringBuilder();
    int[] count = new int[26];
    boolean[] chars = new boolean[26];
    for (char c : s.toCharArray()) {
      count[c - 'a'] += 1;
    }
    for (int i = 0, j = 0; i < s.length(); i++) {
      char curr = s.charAt(i);
      if (!chars[curr - 'a']) {
        while (j > 0 && sb.charAt(j - 1) > curr && count[sb.charAt(j - 1) - 'a'] > 0) {
          chars[sb.charAt(j - 1) - 'a'] = false;
          sb.deleteCharAt(j - 1);
          j--;
        }
        sb.append(curr);
        chars[curr - 'a'] = true;
        j++;
      }
      count[curr - 'a'] -= 1;
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/606896008/){:target="_blank"}

# 설명
1. 주어진 문자열 s를 이용하여 각 문자의 중복을 제거하고, 문자열의 오름차순으로 정렬하여 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sb는 주어진 문자열 s의 중복 제거된 문자열을 동적으로 넣기 위한 변수이다.
  - 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.
- count는 주어진 문자열 s를 알파벳 순서로 존재했는지를 지정하기 위한 변수로, 알파벳 개수인 26으로 크기를 초기화한다.
- chars는 특정 알파벳 문자가 존재했는지 여부를 저장하기 위한 변수로, 알파벳 개수인 26으로 크기를 초기화한다.

3. s를 반복하여 0(a)부터 25(z)까지 문자의 발생 빈도를 count에 넣어준다.

4. 반복문을 통해 정의한 sb에 오름차순으로 중복제거된 문자열을 넣어준다.
- curr에 s의 i번째 문자열을 넣어준다.
- chars의 $curr - a(97)$번째 값이 false이면 아래를 수행한다.
  - j가 0보다 크고, sb의 $j - 1$의 ASCII 값이 curr보다 크면서 sb의 $j - 1$번째 문자에 a(97)를 뺀 값이 0보다 큰 경우 count의 $j - 1$번째 문자에 a(97)를 뺀 위치에 false를 넣고, sb에서 $j - 1$번째 값을 제거하고 j를 감소시킨다.
  - sb에 curr을 넣어주고, chars의 $curr - a(97)$번째 값에 true를 넣어주고, j를 증가시킨다.
- 반복이 종료되면 count의 $curr - a(97)$번째 값을 감소시킨다.

5. 반복이 종료되면 중복을 제거한 오름차순 정렬된 문자의 조합을 넣은 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveDuplicateLetters.java){:target="_blank"}에서 확인 가능합니다.