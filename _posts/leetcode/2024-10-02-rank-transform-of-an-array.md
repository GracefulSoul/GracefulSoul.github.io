---
title: "Leetcode Java Rank Transform of an Array"
excerpt: "Leetcode Rank Transform of an Array Java"
last_modified_at: 2024-10-02T23:30:00
header:
  image: /assets/images/leetcode/rank-transform-of-an-array.png
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
[Link](https://leetcode.com/problems/rank-transform-of-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] arrayRankTransform(int[] arr) {
    int[] sortedArr = arr.clone();
    Arrays.sort(sortedArr);
    Map<Integer, Integer> map = new HashMap<>();
    int rank = 1;
    for (int val : sortedArr) {
      if (!map.containsKey(val)) {
        map.put(val, rank++);
      }
    }
    int length = arr.length;
    int[] result = new int[length];
    for (int i = 0; i < length; i++) {
      result[i] = map.get(arr[i]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/rank-transform-of-an-array/submissions/1409446788/){:target="_blank"}

# 설명
1. arr의 값들을 작은 순서대로 동일 위치에 1부터 시작하는 순위를 배열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sortedArr는 arr을 정렬하여 저장할 변수로, arr을 복사하여 넣어준 후 오름차순 정렬한다.
- map은 값과 순위를 키와 값으로 저장할 변수로, HashMap으로 초기화한다.
- rank는 순위를 계산할 변수로, 시작 순위인 1로 초기화 후 아래를 수행한다.
  - soaredArr의 각 값을 순차적으로 val에 넣어 map의 val에 해당하는 값이 없으면 해당 값에 rank를 넣고 rank를 증가시켜준다.
- length는 arr의 길이를 저장한 변수이다.
- result는 결과를 반환하기 위한 변수로, length 크기의 정수 배열로 초기화한다.

4. 0부터 length 미만까지 i를 증가시키며 result[i]에 map의 arr[i]에 해당 하는 값인 순위를 넣어준 후 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RankTransformOfAnArray.java){:target="_blank"}에서 확인 가능합니다.