---
title: "Leetcode Java Two City Scheduling"
excerpt: "Leetcode Two City Scheduling Java"
last_modified_at: 2024-01-26T20:30:00
header:
  image: /assets/images/leetcode/two-city-scheduling.png
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
[Link](https://leetcode.com/problems/two-city-scheduling){:target="_blank"}

# 코드
```java
class Solution {

  public int twoCitySchedCost(int[][] costs) {
    int length = costs.length / 2;
    int[] dp = new int[length * 2];
    int result = 0;
    int index = 0;
    for (int[] cost : costs) {
      dp[index++] = cost[1] - cost[0];
      result += cost[0];
    }
    Arrays.sort(dp);
    for (int i = 0; i < length; i++) {
      result += dp[i];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/two-city-scheduling/submissions/1157348173/){:target="_blank"}

# 설명
1. 아래를 만족하는 costs에 해당하는 2n명의 직원들을 각 도시에 n명씩 도착하기 위한 최소 비용을 구하는 문제이다.
- costs[i] = [aCost<sub>i</sub>, bCost<sub>i</sub>] 를 만족할 때, 각 값은 아래를 의미한다.
  - aCost<sub>i</sub>는 i번째 직원이 a 도시로 이동하기 위한 비용을 나타낸다.
  - bCost<sub>i</sub>는 i번째 직원이 b 도시로 이동하기 위한 비용을 나타낸다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 각 도시에 도착하기 위한 인원들을 저장할 변수로, costs의 길이를 2로 나눈 값을 저장한다.
- dp는 최소 비용을 계산하기 위한 배열로, $length \times 2$ 크기의 정수 배열로 초기화한다.
- result는 최소 비용을 저장할 변수로, 0으로 초기화한다.
- index는 dp의 위치 값을 저장할 변수로, 0으로 초기화한다.

3. costs의 모든 값을 순차적으로 cost에 넣고 아래를 수행한다.
- dp[index]의 위치에 $cost[1] - cost[0]$인 b 도시로 이동하는 비용과 a 도시로 이동하는 비용의 차이를 저장하고 index를 증가시켜준다.
- result에 a 도시로 이동하는 비용인 cost[0]을 더해준다.

4. dp를 오름차순으로 저장하여 b 도시로 이동하는 비용이 비교적 낮은 오름차순으로 정렬해준다.

5. 정렬된 dp의 앞의 절반 값을 result에 더해주면서 b도시로 이동하기 위한 기회비용을 계산하여 주어진 문제의 결과로 반환한다.

# 해설
- a 도시로 가는 비용을 모두 더한 후, dp에는 a 도시로 가는 비용에서 b 도시로 가는 비용을 뺀 b 도시로 가기 위한 기회(환불)비용이 큰 순서대로 넣어준다.
- a 도시로 가는 비용을 저장한 result에서 위의 dp 내 기회(환불)비용이 가장 큰 절반 값을 더하면 최소 비용을 구할 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TwoCityScheduling.java){:target="_blank"}에서 확인 가능합니다.