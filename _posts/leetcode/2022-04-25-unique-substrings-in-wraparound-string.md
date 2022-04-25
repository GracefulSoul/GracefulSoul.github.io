---
title: "Leetcode Java Unique Substrings in Wraparound String"
excerpt: "Leetcode Unique Substrings in Wraparound String Java 풀이"
last_modified_at: 2022-04-25T12:00:00
header:
  image: /assets/images/leetcode/unique-substrings-in-wraparound-string.png
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
[Link](https://leetcode.com/problems/unique-substrings-in-wraparound-string/){:target="_blank"}

# 코드
```java
class Solution {

  public int findSubstringInWraproundString(String p) {
    char[] charArray = p.toCharArray();
    int[] max = new int[26];
    max[charArray[0] - 'a'] = 1;
    int sum = 1;
    int length = 1;
    for (int idx = 1; idx < p.length(); idx++) {
      int diff = charArray[idx] - charArray[idx - 1];
      if (diff == 1 || diff == -25) {
        length++;
      } else {
        length = 1;
      }
      int index = charArray[idx] - 'a';
      if (length > max[index]) {
        sum += length - max[index];
        max[index] = length;
      }
    }
    return sum;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/686925925/){:target="_blank"}

# 설명
1. 문자열 s에 존재하는 문자열 p의 고유한 하위 부분 문자열의 수를 구하는 문제이다.
- 문자열 s는 "...zabcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyzabcd..."처럼 알파벳 소문자인 "abcdefghijklmnopqrstuvwxyz"가 이어져 있는 문자열이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 p를 문자의 배열로 보관할 변수로, p를 문자의 배열로 변환하여 넣어준다.
- max는 charArray의 문자 별 최대 고유 하위 문자열의 길이를 저장할 변수로, 영문자의 갯수인 26 크기로 초기화하고 charArray의 첫 번째 문자에 'a'를 뺀 위치에 1을 넣어준다.
- sum은 고유한 하위 문자열의 수를 계산할 변수로, 첫 번째 문자가 위에서 포함되었으므로 1로 초기화한다.
- length는 고유한 하위 문자열의 길이를 저장할 변수로, sum과 동일한 이유로 1로 초기화한다.

3. 1부터 p의 길이 전까지 idx를 증가시키며 아래를 반복 수행한다.
- charArray의 idx번째 값과 $idx -1$번째 값의 차이가 1이거나 -25인 경우, length를 증가시킨다.
- 위의 경우가 아니라면 length를 1로 초기화 시킨다.
- index에 charArray의 idx번째 값에 'a'를 뺀 값을 넣어준다.
- length가 max의 index번째 값보다 큰 경우, sum에 $length - max[index]$ 값을 더해주고 max의 index번째 위치에 length를 넣어준다.

4. 반복이 완료되면 고유한 하위 부분 문자열의 수인 sum을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniqueSubstringsInWraparoundString.java){:target="_blank"}에서 확인 가능합니다.