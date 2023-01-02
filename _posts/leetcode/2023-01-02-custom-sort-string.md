---
title: "Leetcode Java Custom Sort String"
excerpt: "Leetcode Custom Sort String Java"
last_modified_at: 2023-01-02T20:45:00
header:
  image: /assets/images/leetcode/custom-sort-string.png
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
[Link](https://leetcode.com/problems/custom-sort-string){:target="_blank"}

# 코드
```java
class Solution {

  public String customSortString(String order, String s) {
    int[] count = new int[26];
    for (char c : s.toCharArray()) {
      count[c - 'a']++;
    }
    StringBuilder sb = new StringBuilder();
    for (char c : order.toCharArray()) {
      while (count[c - 'a']-- > 0) {
        sb.append(c);
      }
    }
    for (int idx = 0; idx < count.length; idx++) {
      while (count[idx]-- > 0) {
        sb.append((char) ('a' + idx));
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/custom-sort-string/submissions/869661453/){:target="_blank"}

# 설명
1. s 문자열을 이용하여 order 문자열의 각 문자의 순서대로 정렬된 문자열을 만드는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count 배열은 s 문자열의 각 문자 갯수를 저장할 변수로, 알파벳 갯수인 26 크기로 초기화하여 s의 각 문자 갯수를 넣어준다.
- sb는 정렬된 문자열을 동적으로 만들기 위한 변수로, StringBuilder로 초기화한다.

3. order의 모든 문자열을 c에 넣어 아래를 반복한다.
- count에서 c의 영문자 순서에 해당하는 횟수만큼 sb에 c를 이어준다.

4. 3번이 완료되면 0부터 count의 길이까지 아래를 반복한다.
- count에 남아있는 값이 있으면 차례대로 sb에 해당 순서에 해당하는 영문자로 변환하여 이어준다.

5. 모든 수행이 완료되어 order의 문자 순으로 정렬된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CustomSortString.java){:target="_blank"}에서 확인 가능합니다.