---
title: "Leetcode Java Average Waiting Time"
excerpt: "Leetcode Medium - 'Average Waiting Time' 문제 Java 풀이"
last_modified_at: 2024-07-09T18:00:00
header:
  image: /assets/images/leetcode/average-waiting-time.png
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
[Link](https://leetcode.com/problems/average-waiting-time/){:target="_blank"}

# 코드
```java
class Solution {

  public double averageWaitingTime(int[][] customers) {
    int time = 0;
    double wait = 0;
    for (int[] customer : customers) {
      time = Math.max(time, customer[0]) + customer[1];
      wait += time - customer[0];
    }
    return wait / customers.length;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/average-waiting-time/submissions/1314956293/){:target="_blank"}

# 설명
1. customers를 이용하여 모든 고객의 평균 대기 시간을 구하는 문제이다.
- customers[i] = [arrival<sub>i</sub>, time<sub>i</sub>] 로, 각 값은 아래를 의미한다.
  - arrival<sub>i</sub>는 i번째 고객의 도착 시간을 의미한다.
  - time<sub>i</sub>는 i번째 고객의 주문을 준비하는데 걸리는 시간을 의미한다.
- 고객이 도착하면 요리사에게 바로 주문을 하고, 고객의 도착 순서대로 하나씩 요리한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- time은 요리를 준비하는 시간을 저장할 변수로, 0으로 초기화한다.
- wait는 요리를 준비하는데 걸리는 시간을 계산할 변수로, 실수형의 0으로 초기화한다.

3. customers의 각 값을 customer에 넣고 순차적으로 아래를 수행한다.
- time에 time과 customer[0]의 값 중 큰 시작 시간에 customer[1]의 값인 요리하는데 걸리는 시간을 더해준다.
- wait에 time과 customer[0]의 차잇값인 고객이 도착 후 요리를 받을 때 까지 걸리는 시간을 더해준다.

4. 반복이 완료되면 저장된 wait에 customers의 길이를 나누어 평균 대기 시간을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AverageWaitingTime.java){:target="_blank"}에서 확인 가능합니다.