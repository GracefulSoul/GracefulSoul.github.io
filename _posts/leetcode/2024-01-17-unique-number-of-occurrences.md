---
title: "Leetcode Java Unique Number of Occurrences"
excerpt: "Leetcode Easy - 'Unique Number of Occurrences' 문제 Java 풀이"
last_modified_at: 2024-01-17T18:40:00
header:
  image: /assets/images/leetcode/unique-number-of-occurrences.png
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
[Link](https://leetcode.com/problems/unique-number-of-occurrences){:target="_blank"}

# 코드
```java
class Solution {

  public boolean uniqueOccurrences(int[] arr) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int num : arr) {
      map.put(num, map.getOrDefault(num, 0) + 1);
    }
    Set<Integer> set = new HashSet<>();
    for (int value : map.values()) {
      if (!set.add(value)) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/unique-number-of-occurrences/submissions/1148652467/){:target="_blank"}

# 설명
1. arr의 각 숫자들이 고유한 갯수로 나타나는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 arr의 각 숫자 별 갯수를 계산하기 위한 변수로, HashMap으로 초기화하고 arr을 반복하여 갯수를 계산해준다.
- set은 갯수가 고유한지 검증하기 위한 변수로, HashSet으로 초기화한다.

3. map의 value들을 반복하여 set에 value를 넣어주다가 존재하는 값이 존재하면, false를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 각 숫자가 고유한 갯수로 존재하므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniqueNumberOfOccurrences.java){:target="_blank"}에서 확인 가능합니다.