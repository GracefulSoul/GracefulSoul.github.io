---
title: "Leetcode Java Find Longest Special Substring That Occurs Thrice I"
excerpt: "Leetcode - 'Find Longest Special Substring That Occurs Thrice I' 문제 Java 풀이"
last_modified_at: 2024-12-10T19:30:00
header:
  image: /assets/images/leetcode/find-longest-special-substring-that-occurs-thrice-i.png
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
[Link](https://leetcode.com/problems/find-longest-special-substring-that-occurs-thrice-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumLength(String s) {
    int length = s.length();
    int start = 1;
    int end = length;
    if (!this.isLeastThriceOccurs(s, length, start)) {
      return -1;
    }
    while (start + 1 < end) {
      int mid = (start + end) / 2;
      if (this.isLeastThriceOccurs(s, length, mid)) {
        start = mid;
      } else {
        end = mid;
      }
    }
    return start;
  }

  private boolean isLeastThriceOccurs(String s, int length, int num) {
    int[] counts = new int[26];
    int start = 0;
    for (int i = 0; i < length; i++) {
      while (s.charAt(start) != s.charAt(i)) {
        start++;
      }
      int index = s.charAt(i) - 'a';
      if (i - start + 1 >= num) {
        counts[index]++;
      }
      if (counts[index] > 2) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-longest-special-substring-that-occurs-thrice-i/submissions/1475156615/){:target="_blank"}

# 설명
1. 문자열 s에서 동일 문자로 이루어진 부분 문자열이 해당 문자열에서 최소 세 번 반복되기 위한 최대 길이를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 문자열 s의 길이를 저장한 변수이다.
- start와 end는 문자열 탐색에 필요한 변수로, 1과 length로 초기화한다.

3. 최소 세 번 이상 문자열에 존재하는지 검증하는 메서드인 isLeastThriceOccurs(String s, int length, int num)를 정의한다.
- 검증에 필요한 변수를 정의한다.
  - counts는 영문자 갯수를 저장할 변수로, 26 크기의 정수 배열로 초기화한다.
  - start는 탐색 시작에 필요한 변수로, 0으로 초기화한다.
- 0부터 length 미만까지 i를 증가시키면서 아래를 반복한다.
  - s의 start번째 문자와 i번째 문자가 다른 경우, start를 증가시키며 동일한 문자 위치까지 이동시킨다.
  - index에 s의 i번째 영문자의 0-index 순서를 넣어준다.
  - $i - start + 1$이 num 이상인 부분 문자열에 해당하는 경우, counts[index]를 증가시켜준다.
  - counts[index]가 2 초과인 조건을 만족하는 경우, true를 반환한다.
- 반복이 완료되면 조건을 만족하지 않으므로, false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindLongestSpecialSubstringThatOccursThriceI.java){:target="_blank"}에서 확인 가능합니다.