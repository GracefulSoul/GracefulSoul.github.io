---
title: "Leetcode Java Count Unique Characters of All Substrings of a Given String"
excerpt: "Leetcode Count Unique Characters of All Substrings of a Given String Java"
last_modified_at: 2023-02-04T08:40:00
header:
  image: /assets/images/leetcode/count-unique-characters-of-all-substrings-of-a-given-string.png
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
[Link](https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string){:target="_blank"}

# 코드
```java
class Solution {

  public int uniqueLetterString(String s) {
    int[] curr = new int[26];
    Arrays.fill(curr, -1);
    int[] last = new int[26];
    Arrays.fill(last, -1);
    int count = 0;
    int result = 0;
    for (int i = 0; i < s.length(); i++) {
      int j = s.charAt(i) - 'A';
      count += i - curr[j] + last[j] - curr[j];
      last[j] = curr[j];
      curr[j] = i;
      result += count;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-unique-characters-of-all-substrings-of-a-given-string/submissions/890967443/){:target="_blank"}

# 설명
1. s의 연속된 부분 문자열들 내 고유 문자열의 개수를 모두 더하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- curr은 이전 문자열까지 계산된 부분 문자열의 수를 저장할 변수로, 영문자의 개수은 26 크기로 초기화하고 -1을 채워준다.
- last는 curr 이전 문자열까지 계산된 부분 문자열의 수를 저장한 변수로, 영문자의 개수은 26 크기로 초기화하고 -1을 채워준다.
- count는 부분 문자열의 수를 누계할 변수로, 0으로 초기화한다.
- result는 연속된 부분 문자열들 내 고유 문자열의 개수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 s길이 미만까지 i를 증가시키며 아래를 수행한다.
- j에 s의 i번째 문자의 영문자 순서를 넣어준다.
- count에 i와 curr의 j번째 값의 차이와 last의 j번째 값에 curr의 j번째 값의 차이를 더하여 누계하여, 해당 위치에 해당하는 부분 문자열들의 고유 문자열 수를 count에 누계한다.
- last의 j번째 위치에 curr의 j번째 값을 저장하여 값을 백업한다.
- curr의 j번째 위치에 i를 넣어 현재 위치를 저장한다.
- result에 현재 위치에 해당하는 부분 문자열들의 고유 문자열 수를 저장한 count를 더해준다.

4. 반복이 완료되면 연속된 부분 문자열들 내 고유 문자열의 개수를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountUniqueCharactersOfAllSubstringsOfAGivenString.java){:target="_blank"}에서 확인 가능합니다.