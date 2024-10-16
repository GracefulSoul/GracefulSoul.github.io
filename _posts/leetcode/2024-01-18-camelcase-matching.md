---
title: "Leetcode Java Camelcase Matching"
excerpt: "Leetcode Camelcase Matching Java"
last_modified_at: 2024-01-18T18:15:00
header:
  image: /assets/images/leetcode/camelcase-matching.png
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
[Link](https://leetcode.com/problems/camelcase-matching){:target="_blank"}

# 코드
```java
class Solution {

  public List<Boolean> camelMatch(String[] queries, String pattern) {
    List<Boolean> result = new ArrayList<>();
    for (String query : queries) {
      result.add(this.isMatch(query, pattern));
    }
    return result;
  }

  private boolean isMatch(String query, String pattern) {
    int i = 0;
    for (char c : query.toCharArray()) {
      if (i < pattern.length() && c == pattern.charAt(i)) {
        i++;
      } else if (c < 'a') {
        return false;
      }
    }
    return i == pattern.length();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/camelcase-matching/submissions/1149611885/){:target="_blank"}

# 설명
1. 문자열 배열인 queries 내 pattern에 해당하는 대문자 순서대로의 문자열인지 검증하는 문제이다.

2. result는 결과를 저장할 변수이다.

3. queries의 각 문자열을 query에 순차적으로 넣어 4번에서 정의한 isMatch(String query, String pattern) 메서드를 수행한 결과를 result에 넣어준다.

4. query가 pattern에 해당하는 형태의 문자열인지 검증하기 위한 isMatch(String query, String pattern) 메서드를 정의한다.
- i는 pattern 문자열의 위치 값을 저장할 변수로, 0으로 초기화한다.
- query의 각 값을 c에 넣어 아래를 반복한다.
  - i가 pattern 길이 미만이면서 c가 pattern의 i번째 문자와 동일한 경우, i를 증가시켜준다.
  - 위의 경우가 아니면서 c가 'a'문자열보다 작은 영대문자에 속하는 경우, false를 반환한다.
- 반복이 완료되면 i가 pattern의 마지막 위치인지 검증한 결과를 반환한다.

5. 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CamelcaseMatching.java){:target="_blank"}에서 확인 가능합니다.