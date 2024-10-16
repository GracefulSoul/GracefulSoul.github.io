---
title: "Leetcode Java Longest Substring with At Least K Repeating Characters"
excerpt: "Leetcode Longest Substring with At Least K Repeating Characters Java 풀이"
last_modified_at: 2022-02-23T18:00:00
header:
  image: /assets/images/leetcode/longest-substring-with-at-least-k-repeating-characters.png
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
[Link](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestSubstring(String s, int k) {
    return this.recursive(s, k, 0, s.length());
  }

  private int recursive(String s, int k, int start, int end) {
    if (end < k) {
      return 0;
    }
    int[] count = new int[26];
    char[] charArray = s.toCharArray();
    for (int i = start; i < end; i++) {
      count[charArray[i] - 'a']++;
    }
    for (int mid = start; mid < end; mid++) {
      if (count[charArray[mid] - 'a'] >= k) {
        continue;
      }
      int next = mid + 1;
      while (next < end && count[charArray[next] - 'a'] < k) {
        next++;
      }
      return Math.max(this.recursive(s, k, start, mid), this.recursive(s, k, next, end));
    }
    return end - start;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/647324741/){:target="_blank"}

# 설명
1. 주어진 문자열 s 중 k번 이상 반복된 문자열이 들어간 가장 긴 부분 문자열의 길이를 구하는 문제이다.

2. 재귀 호출을 위한 recursive(String s, int k, int start, int end) 메서드를 이용하여 0부터 s의 길이까지 가장 긴 부분 문자열의 길이를 주어진 문제의 결과로 반환한다.
- end가 k보다 작은 경우 k번 이상 반복할 문자가 존재하지 않으므로, 0을 반환한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - count는 각 문자 별 발생 횟수를 저장하기 위한 배열로, 알파벳의 개수인 26 크기로 정의한다.
  - charArray는 s를 문자의 배열로 변환하여 저장한다.
- start부터 end까지 count 배열 내 영문자의 순서인 'a'(0) ~ 'z'(25)에 발생 횟수를 저장한다.
- start부터 end까지 mid를 증가시키며 반복을 수행한다.
  - charArray의 mid번째 문자가 k 이상인 경우 조건을 만족하므로, 반복을 계속 수행한다.
  - next에 $mid + 1$을 넣어준다.
  - next가 end 미만이고 charArray의 next번째 문자의 개수가 k개 미만인 경우, next를 증가시킨다.
  - start에서 mid, next에서 end까지 각각 재귀 호출을 수행하여 가장 큰 값을 반환한다.
- 반복이 정상적으로 끝나면 가장 큰 길이가 되는, $end - start$를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestSubstringWithAtLeastKRepeatingCharacters.java){:target="_blank"}에서 확인 가능합니다.