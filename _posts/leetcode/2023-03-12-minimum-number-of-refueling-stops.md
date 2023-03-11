---
title: "Leetcode Java Minimum Number of Refueling Stops"
excerpt: "Leetcode Minimum Number of Refueling Stops Java"
last_modified_at: 2023-03-12T07:50:00
header:
  image: /assets/images/leetcode/minimum-number-of-refueling-stops.png
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
[Link](https://leetcode.com/problems/minimum-number-of-refueling-stops){:target="_blank"}

# 코드
```java
class Solution {

  public int minRefuelStops(int target, int startFuel, int[][] stations) {
    Queue<Integer> queue = new PriorityQueue<>();
    int i = 0;
    int result = 0;
    while (startFuel < target) {
      while (i < stations.length && stations[i][0] <= startFuel) {
        queue.offer(-stations[i++][1]);
      }
      if (queue.isEmpty()) {
        return -1;
      }
      startFuel -= queue.poll();
      result++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-refueling-stops/submissions/913448455/){:target="_blank"}

# 설명
1. startFuel만큼 주유된 차량으로 stations의 주유소를 거쳐 target까지 도착하기까지 최소 주유 횟수를 구하는 문제이다.
- target까지 도착할 수 없는 경우, -1을 주어진 문제의 결과로 반환한다.
- stations[i] = [position<sub>i</sub>, fuel<sub>i</sub>]로, position<sub>i</sub>는 주유소의 위치 fuel<sub>i</sub>는 주유 용량을 의미한다.
- 1의 거리를 이동하기 위해 1의 주유 용량을 소모한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- queue는 현재 주유된 용량 내 도착할 수 있는 주유소의 주유 용량을 저장하기 위한 변수로, 주유 용량을 오름차순으로 정렬해서 저장하기 위해 PriorityQueue로 초기화한다.
- i는 stations의 탐색 위치를 저장할 변수로, 처음 위치인 0으로 초기화한다.
- result는 최소 주유 횟수를 저장하기 위한 변수로, 0으로 초기화한다.

3. startFuel이 target이 되기 전까지 아래를 반복한다.
- i가 stations의 길이 미만으로 모두 탐색한 상태가 아니면서 stations[i][0]가 startFuel이하인 도착 가능한 주유소인 경우, queue에 해당 주유소의 주유 용량인 stations[i][1]을 음수로 넣어주고 i를 증가시킨다.
- queue가 비어있는 경우 target까지 도착하기 전에 주유된 용량을 모두 소모하므로, -1을 주어진 문제의 결과로 반환한다.
- startFuel에 queue에서 가장 작은 값을 꺼내 빼주고 result를 증가시킨다.

4. 반복이 완료되면 최소 주유 횟수가 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfRefuelingStops.java){:target="_blank"}에서 확인 가능합니다.