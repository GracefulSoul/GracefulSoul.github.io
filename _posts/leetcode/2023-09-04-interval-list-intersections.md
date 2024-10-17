---
title: "Leetcode Java Sum of Even Numbers After Queries"
excerpt: "Leetcode Medium - 'Sum of Even Numbers After Queries' 문제 Java 풀이"
last_modified_at: 2023-09-04T18:50:00
header:
  image: /assets/images/leetcode/interval-list-intersections.png
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
[Link](https://leetcode.com/problems/interval-list-intersections){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
    List<int[]> result = new ArrayList<>();
    for (int i = 0, j = 0; i < firstList.length && j < secondList.length;) {
      int start = Math.max(firstList[i][0], secondList[j][0]);
      int end = Math.min(firstList[i][1], secondList[j][1]);
      if (start <= end) {
        result.add(new int[] { start, end });
      }
      if (firstList[i][1] < secondList[j][1]) {
        i++;
      } else {
        j++;
      }
    }
    return result.toArray(new int[0][0]);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/interval-list-intersections/submissions/1040169324/){:target="_blank"}

# 설명
1. [start, end]로 이루어진 firstList와 secondList를 이용하여 겹치는 지점을 찾는 문제이다.

2. result는 겹치는 구간을 저장할 변수로, ArrayList로 초기화한다.

3. i와 j는 두 배열의 위치 변수로, 0부터 둘 중 하나라도 마지막까지 수행할 때 까지 아래를 반복한다.
- start에 각 배열의 시작 위치인 firstList[i][0], secondList[j][0] 중 큰 값을 넣어준다.
- end에 각 배열의 종료 위치인 firstList[i][1], secondList[j][1] 중 작은 값을 넣어준다.
- 만일 start가 end보다 같거나 작은 경우, result에 [start, end]로 넣어준다.
- 종료 위치인 firstList[i][1]가 secondList[j][1] 보다 작은 경우, i를 증가시키고 크면 j를 증가시킨다.

4. 반복이 완료되면 result를 2차원 배열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IntervalListIntersections.java){:target="_blank"}에서 확인 가능합니다.