---
title: "Leetcode Java Kth Distinct String in an Array"
excerpt: "Leetcode Easy - 'Kth Distinct String in an Array' 문제 Java 풀이"
last_modified_at: 2024-08-05T18:30:00
header:
  image: /assets/images/leetcode/kth-distinct-string-in-an-array.png
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
[Link](https://leetcode.com/problems/kth-distinct-string-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public String kthDistinct(String[] arr, int k) {
    Map<String, Integer> map = new HashMap<>();
    for (String s : arr) {
      map.put(s, map.getOrDefault(s, 0) + 1);
    }
    for (String s : arr) {
      if (map.get(s) == 1 && --k == 0) {
        return s;
      }
    }
    return "";
  }

}
```

# 결과
[Link](https://leetcode.com/problems/kth-distinct-string-in-an-array/submissions/1345185021/){:target="_blank"}

# 설명
1. arr 내 고유하게 존재하는 k번째 문자열을 반환하는 문제이다.

2. map은 문자열의 갯수를 젖아할 변수로, HashMap으로 초기화하여 arr을 반복하여 s를 키로 arr 내 동일 문자열 갯수를 값으로 넣어준다.

3. arr의 값들을 s에 순차적으로 넣어 아래를 수행한다.
- map에서 s의 값이 1인 고유 문자열이면서 k를 감소시킨 값이 0이 되는 k번째 문자열이면, s를 주어진 문제의 결과로 반환한다.

4. 위의 반복이 완료되면 만족하는 문자열이 없으므로 빈 문자열("")을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KthDistinctStringInAnArray.java){:target="_blank"}에서 확인 가능합니다.