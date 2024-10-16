---
title: "Leetcode Java Gas Station"
excerpt: "Leetcode Gas Station Java 풀이"
last_modified_at: 2021-08-23T13:00:00
header:
  image: /assets/images/leetcode/gas-station.png
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
[Link](https://leetcode.com/problems/gas-station/){:target="_blank"}

# 코드
```java
class Solution {

  public int canCompleteCircuit(int[] gas, int[] cost) {
    int fill = 0;
    int use = 0;
    int tank = 0;
    int start = 0;
    for (int idx = 0; idx < gas.length; idx++) {
      fill += gas[idx];
      use += cost[idx];
      tank += gas[idx] - cost[idx];
      if (tank < 0) {
        tank = 0;
        start = idx + 1;
      }
    }
    return fill < use ? -1 : start;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/542674987/){:target="_blank"}

# 설명
1. 주어진 정수 배열 gas는 해당 위치에서 주유할 수 있는 양이고, cost는 해당 위치까지 이동하기 위해 사용되는 가스의 양을 의미하여 한 바퀴 순회하기 위한 시작 index를 찾는 문제이다.
- 단, 한 바퀴 순회가 불가능하다면 -1을 주어진 문제의 결과로 반환해야 한다.
- 또한 모든 문제에는 유일한 결과만 존재한다.

2. 주어진 문제를 풀기 위한 변수를 정의한다.
- fill은 주유소에 도달하여 채우는 gas의 합을 저장한다.
- use는 다음 주유소까지 이동하기 위해 사용되는 cost의 합을 저장한다.
- tank는 자동차에 남은 가스의 양을 나타낸다.
- start는 한 바퀴 순회하기 위한 시작 index를 저장한다.

3. 주어진 배열 gas 혹은 cost의 길이만큼 반복하여 각 변수에 해당하는 값들을 저장한다.
- 주유소에서 채우는 양을 저장하는 변수 fill에 idx번째 gas를 누계한다.
- 이동하기 위해 사용되는 변수 use에 idx번째 cost를 누계한다.
- 자동차에 남은 가스의 양을 나타내는 변수 tank에 idx번째 gas와 idx번째 cost의 차이를 누계한다.
- tank가 0 미만으로 내려간 경우 idx번째 위치까지 이동이 불가능하므로, 시작 위치를 저장하는 변수 start를 다음 위치인 $idx + 1$로 바꾸어주고 tank는 0으로 초기화 시킨다.

4. 반복이 완료되면 주유한 양을 저장한 fill과 사용한 양을 저장한 use을 비교하여 주어진 문제여 결과를 반환한다.
- 변수 fill보다 use가 더 큰 경우 순회가 불가능하므로, -1을 주어진 문제의 결과로 반환한다.
- 변수 fill보다 use가 작거나 같은 경우 순회가 가능하므로, 시작 위치를 저장한 start를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GasStation.java){:target="_blank"}에서 확인 가능합니다.