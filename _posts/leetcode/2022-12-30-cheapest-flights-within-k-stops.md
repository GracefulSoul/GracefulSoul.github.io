---
title: "Leetcode Java Cheapest Flights Within K Stops"
excerpt: "Leetcode - 'Cheapest Flights Within K Stops' 문제 Java 풀이"
last_modified_at: 2022-12-30T12:50:00
header:
  image: /assets/images/leetcode/cheapest-flights-within-k-stops.png
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
[Link](https://leetcode.com/problems/cheapest-flights-within-k-stops){:target="_blank"}

# 코드
```java
class Solution {

  public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
    int[] dp = new int[n];
    Arrays.fill(dp, Integer.MAX_VALUE);
    dp[src] = 0;
    while (k-- >= 0) {
      if (this.isExistsRoute(flights, dp)) {
        break;
      }
    }
    return dp[dst] == Integer.MAX_VALUE ? -1 : dp[dst];
  }

  private boolean isExistsRoute(int[][] flights, int[] dp) {
    int[] temp = Arrays.copyOf(dp, dp.length);
    boolean result = true;
    for (int[] flight : flights) {
      int src = flight[0];
      int dst = flight[1];
      int cost = flight[2];
      if (temp[src] < Integer.MAX_VALUE && dp[dst] > dp[src] + cost) {
        dp[dst] = temp[src] + cost;
        result = false;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/cheapest-flights-within-k-stops/submissions/867880088/){:target="_blank"}

# 설명
1. n개의 도시 중 k번 멈춰서 src에서 출발하여 dst에 도착하기 위해 가장 저렴한 가격을 찾는 문제이다.
- 항공편 정보가 담긴 flights는 flights[i] = [from<sub>i</sub>, to<sub>i</sub>, price<sub>i</sub>]를 만족한다.
- 가장 저렴한 가격이 없는 경우, -1을 주어진 문제의 결과로 반환한다.

2. dp는 최소 가격을 구하기 위해 사용할 정수 배열로, n 크기로 정의하여 첫 값은 0 나머지는 정수의 최댓값을 넣어준다.

3. k가 0보다 클 때 까지 k를 감소시키며 아래를 반복한다.
- 만일 flights와 dp를 이용하여 4번에서 정의한 isExistsRoute(int[][] flights, int[] dp) 메서드를 수행한 결과가 true이면 반복을 중지시킨다.

4. 최소 비용을 dp에 저장하고 경로가 존재하는지 검증하기 위한 isExistsRoute(int[][] flights, int[] dp) 메서드를 정의한다.
- temp에 dp를 Deep copy하여 넣어준다.
- 경로가 존재하는지 여부를 저장한 result를 true로 임시 저장한다.
- flights의 모든 값을 flight에 넣어 아래를 반복한다.
  - src와 dst, cost에 flight의 모든 값을 순차적으로 넣어준다.
  - temp의 src번째 값이 정수의 최댓값이면서 dp의 dst번째 값이 src번째 값과 cost를 더한 값보다 큰 경우, dp의 dst번째 위치에 temp의 src번째 값과 cost를 더한 값을 넣고 result를 false로 바꾸어준다.
- 반복이 완료되면 result를 반환한다.

5. 3번의 반복이 완료되면 dp의 dst번째 값이 정수의 최댓값인 경우 경로가 존재하지 않으므로 -1을, 존재하면 해당 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheapestFlightsWithinKStops.java){:target="_blank"}에서 확인 가능합니다.