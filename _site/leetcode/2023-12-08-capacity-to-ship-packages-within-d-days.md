---
title: "Leetcode Java Capacity To Ship Packages Within D Days"
excerpt: "Leetcode Capacity To Ship Packages Within D Days Java"
last_modified_at: 2023-12-09T10:40:00
header:
  image: /assets/images/leetcode/capacity-to-ship-packages-within-d-days.png
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
[Link](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days){:target="_blank"}

# 코드
```java
class Solution {

  public int shipWithinDays(int[] weights, int days) {
    int max = 0;
    int sum = 0;
    for (int weight : weights) {
      max = Math.max(max, weight);
      sum += weight;
    }
    while (max < sum) {
      int mid = max + ((sum - max) / 2);
      int need = 1;
      int curr = 0;
      for (int weight : weights) {
        if (curr + weight > mid) {
          need += 1;
          curr = 0;
        }
        curr += weight;
      }
      if (need > days) {
        max = mid + 1;
      } else {
        sum = mid;
      }
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/submissions/1115409456/){:target="_blank"}

# 설명
1. days번 이동할 물건들의 무게인 weights를 최대한 균등한 무게로 나누어 옮기기 위한 선박의 최소 중량을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 물건들 중 가장 큰 무게를 저장할 변수로, weights 내 가장 무거운 무게를 넣어준다.
- sum은 물건들의 총 중량을 저장할 변수로, weights의 모든 값을 더해 넣어준다.

3. max가 sum보다 작을 때 까지 아래를 반복한다.
- mid는 한 번에 이동할 물건의 최대 무게를 저장할 변수로, 중앙값인 $max + \frac{sum - max}{2}$로 초기화한다.
- count는 이동 횟수를 저장할 변수로, 1로 초기화한다.
- curr은 현재 이동할 물건의 무게를 저장할 변수로, 0으로 초기화한다.
- weights를 이용하여 mid만큼의 중량이 되지 않도록 이동하기 위한 count를 계산한다.
- count가 days보다 높은 경우 선박의 중량을 더 높게 측정하기 위해 max에 $mid + 1$을 넣어주고, 반대의 경우 선박의 중량을 더 낮게 측정하기 위해 sum에 mid를 넣어 범위를 축소시킨다.

4. 반복이 완료되면 계산된 선박의 최소 중량인 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CapacityToShipPackagesWithinDDays.java){:target="_blank"}에서 확인 가능합니다.