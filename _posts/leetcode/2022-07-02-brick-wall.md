---
title: "Leetcode Java Brick Wall"
excerpt: "Leetcode Brick Wall Java"
last_modified_at: 2022-07-02T17:00:00
header:
  image: /assets/images/leetcode/brick-wall.png
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
[Link](https://leetcode.com/problems/brick-wall/){:target="_blank"}

# 코드
```java
class Solution {

  public int leastBricks(List<List<Integer>> wall) {
    Map<Integer, Integer> map = new HashMap<>();
    int count = 0;
    for (List<Integer> row : wall) {
      int sum = 0;
      for (int idx = 0; idx < row.size() - 1; idx++) {
        sum += row.get(idx);
        map.put(sum, map.getOrDefault(sum, 0) + 1);
        count = Math.max(count, map.get(sum));
      }
    }
    return wall.size() - count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/736424975/){:target="_blank"}

# 설명
1. 벽의 벽돌을 나타내는 wall을 이용하여 위에서 아래로 직선을 그을 경우 만날 수 있는 최소한의 벽돌의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- 줄을 긋는 위치에 빈 공간의 수를 저장할 map을 정의하고, HashMap으로 초기화한다.
- 벽돌의 빈 공간을 저장할 count를 정의하고, 0으로 초기화한다.

3. wall의 각 행을 row로 아래를 수행한다.
- sum은 현재 가로의 위치를 저장할 변수로, 0으로 초기화한다.
- 마지막 벽돌의 위치는 중요하지 않으므로 0부터 row의 마지막 값을 제외하고 idx를 증가시키며 아래를 수행한다.
  - sum의 row의 idx번째 값을 더한다.
  - map에서 sum에 해당하는 값을 가져오거나 없으면 0을 가져와 1을 증가시킨 값을 map에 다시 저장한다.
  - count에 count와 map의 sum에 해당하는 값 중 큰 값을 넣어준다.

4. 반복이 완료되면 벽돌 층의 수인 wall의 길이에 빈 공간의 수인 count의 차이를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BrickWall.java){:target="_blank"}에서 확인 가능합니다.