---
title: "Leetcode Java Maximum Distance in Arrays"
excerpt: "Leetcode Medium - 'Maximum Distance in Arrays' 문제 Java 풀이"
last_modified_at: 2024-08-16T14:50:00
header:
  image: /assets/images/leetcode/maximum-distance-in-arrays.png
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
[Link](https://leetcode.com/problems/maximum-distance-in-arrays/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxDistance(List<List<Integer>> arrays) {
    int result = 0;
    List<Integer> list = arrays.get(0);
    int min = list.getFirst();
    int max = list.getLast();
    for (int i = 1; i < arrays.size(); i++) {
      list = arrays.get(i);
      int first = list.getFirst();
      int last = list.getLast();
      result = Math.max(result, Math.max(Math.abs(last - min), Math.abs(first - max)));
      min = Math.min(min, first);
      max = Math.max(max, last);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-distance-in-arrays/submissions/1357393283/){:target="_blank"}

# 설명
1. 각 값들이 오름차순으로 정렬된 arrays 내 배열들을 이용하여 두 개의 다른 배열에서 각각 한 값을 꺼내 $|a - b|$인 거리가 가장 큰 최대 거리를 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최대 거리를 저장할 변수로, 0으로 초기화한다.
- min과 max는 arrays의 첫 List에서 첫 값과 마지막 값인 최솟값과 최댓값을 넣은 변수이다.

3. 1부터 arrays의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- first와 last에 arrays의 i번째 List에서 첫 값과 마지막 값인 최솟값과 최댓값을 넣어준다.
- result에 result, $|last - min|$, $|first - max|$ 중 가장 큰 거리의 값을 넣어준다.
- min에 min과 first 중 작은 값을, max에 max와 last 중 큰 값을 넣어준다.

4. 반복이 완료되면 최대 거리가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumDistanceInArrays.java){:target="_blank"}에서 확인 가능합니다.