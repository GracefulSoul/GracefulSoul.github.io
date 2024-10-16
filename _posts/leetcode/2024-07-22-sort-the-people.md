---
title: "Leetcode Java Lucky Numbers in a Matrix"
excerpt: "Leetcode Lucky Numbers in a Matrix Java"
last_modified_at: 2024-07-22T18:20:00
header:
  image: /assets/images/leetcode/sort-the-people.png
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
[Link](https://leetcode.com/problems/sort-the-people/){:target="_blank"}

# 코드
```java
class Solution {

  public String[] sortPeople(String[] names, int[] heights) {
    int length = names.length;
    Map<Integer, String> map = new HashMap<>();
    for (int i = 0; i < length; i++) {
      map.put(heights[i], names[i]);
    }
    Arrays.sort(heights);
    String[] result = new String[length];
    for (int index = 0, i = length - 1; i >= 0; i--, index++) {
      result[index] = map.get(heights[i]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sort-the-people/submissions/1329324966/){:target="_blank"}

# 설명
1. heights의 키를 이용하여 names를 키가 큰 사람 순서대로 정렬하여 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 names의 길이를 저장한 변수이다.
- map은 사람 별 키를 저장할 변수로, 순차적으로 키와 이름을 쌍으로 넣어준다.
- result는 정렬된 사람의 이름을 넣을 변수로, length 크기의 문자열 배열로 초기화한다.

3. index는 0으로, $length - 1$부터 0 이상일 때 까지 i를 감소시키고 index를 증가시키며 result[index]에 map에서 heights[i]의 값인 이름을 꺼내 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LuckyNumbersInAMatrix.java){:target="_blank"}에서 확인 가능합니다.