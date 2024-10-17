---
title: "Leetcode Java Unique Length-3 Palindromic Subsequences"
excerpt: "Leetcode Medium - 'Unique Length-3 Palindromic Subsequences' 문제 Java 풀이"
last_modified_at: 2023-11-14T19:40:00
header:
  image: /assets/images/leetcode/unique-length-3-palindromic-subsequences.png
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
[Link](https://leetcode.com/problems/unique-length-3-palindromic-subsequences){:target="_blank"}

# 코드
```java
class Solution {

  public int countPalindromicSubsequence(String s) {
    int result = 0;
    char[] charArray = s.toCharArray();
    int length = charArray.length;
    for (char c = 'a'; c <= 'z'; c++) {
      int start = -1;
      int end = -1;
      for (int i = 0; i < length; i++) {
        if (charArray[i] == c) {
          if (start == -1) {
            start = i;
          }
          end = i;
        }
      }
      if (start != -1 && end != -1 && end - start >= 2) {
        boolean[] seen = new boolean[26];
        for (int i = start + 1; i < end; i++) {
          int num = charArray[i] - 'a';
          if (!seen[num]) {
            seen[num] = true;
            result++;
          }
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/submissions/1098575584/){:target="_blank"}

# 설명
1. s의 임의 세 문자를 이용하여 만들 수 있는 앞과 뒤가 동일한 문자열인 회문의 중복되지 않은 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 회문의 갯수를 저장할 변수로, 0으로 초기화한다.
- charArray는 s를 문자 배열로 변환하여 저장한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.

3. 'a'부터 'z'까지 c를 증가시키며 아래를 반복한다.
- start와 end를 회문의 시작과 종료 위치를 저장할 변수로, charArray의 문자들을 반복하여 start의 회문의 시작 위치를 넣고 end에 c의 마지막 위치를 넣어준다.
- start와 end가 -1이 아니면서 end와 start의 차이가 2 이상인 최소 3자리 이상인 경우, 아래를 수행한다.
  - seen은 회문의 가운데 문자 중 확인한 문자를 체크하기 위한 변수로, 영문자의 갯수인 26 크기의 부울 배열로 초기화한다.
  - $start + 1$부터 end 미만까지 i를 증가시키며, charArray[i]의 문자가 이전에 존재하지 않은 경우 seen[num]을 true로 변경하고 중복되지 않은 회문의 갯수인 result를 증가시켜 증가시킨다.

4. 반복이 완료되면 중복되지 않은 회문의 갯수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniqueLength3PalindromicSubsequences.java){:target="_blank"}에서 확인 가능합니다.