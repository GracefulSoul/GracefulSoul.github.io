---
title: "Leetcode Java Maximum Running Time of N Computers"
excerpt: "Leetcode Hard - 'Maximum Running Time of N Computers' 문제 Java 풀이"
last_modified_at: 2023-07-26T20:50:00
header:
  image: /assets/images/leetcode/maximum-running-time-of-n-computers.png
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
[Link](https://leetcode.com/problems/maximum-running-time-of-n-computers){:target="_blank"}

# 코드
```java
class Solution {

  public long maxRunTime(int n, int[] batteries) {
    long sum = 0;
    for (int battery : batteries) {
      sum += battery;
    }
    long min = 1;
    long max = (sum / n) + 1;
    while (min < max) {
      long mid = min + ((max - min) / 2);
      sum = 0;
      for (int battery : batteries) {
        sum += Math.min(battery, mid);
      }
      if (sum >= mid * n) {
        min = mid + 1;
      } else {
        max = mid;
      }
    }
    return min - 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-running-time-of-n-computers/submissions/1005222842/){:target="_blank"}

# 설명
1. batteries는 컴퓨터를 실행할 수 있는 시간을 넣은 변수로, n개의 컴퓨터를 동시에 실행할 수 있는 최대 시간을 구하는 문제이다.
- 처음에는 각 컴퓨터에 최대 한 개의 배터리를 삽입하고, 그 이후 교체 시간 없이 임의의 배터리를 교체한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 batteries의 합을 더하기 위한 변수로, batteries의 모든 값을 더해준다.
- min과 max는 시간 탐색에 필요한 변수로, 최소 가능한 시간인 1과 최대 가능한 시간인 $\frac{sum}{n} + 1$로 초기화한다.

3. min이 max 미만일 때까지 아래를 수행한다.
- mid에 $min + \frac{max - min}{2}$의 중앙값을 넣어준다.
- sum을 0으로 초기화하고 batteries의 각 값과 mid 중 작은 값 기준으로 sum에 더해준다.
- sum이 $mid \times n$보다 크거나 같은지 검증하여 아래를 수행한다.
  - 크거나 같으면, min에 $mid + 1$을 넣어 하한 범위를 좁혀준다.
  - 작으면, max에 mid를 넣어 상한 범위를 좁혀준다.

4. 반복이 완료되면 시간이 계산된 min에 1을 빼서 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumRunningTimeOfNComputers.java){:target="_blank"}에서 확인 가능합니다.