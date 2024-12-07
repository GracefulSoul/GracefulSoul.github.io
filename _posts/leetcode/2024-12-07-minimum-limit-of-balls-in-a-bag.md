---
title: "Leetcode Java Minimum Limit of Balls in a Bag"
excerpt: "Leetcode - 'Minimum Limit of Balls in a Bag' 문제 Java 풀이"
last_modified_at: 2024-12-07T17:30:00
header:
  image: /assets/images/leetcode/minimum-limit-of-balls-in-a-bag.png
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
[Link](https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumSize(int[] nums, int maxOperations) {
    int left = 1;
    int right = 1_000_000_000;
    while (left < right) {
      int mid = (left + right) / 2;
      int count = 0;
      for (int num : nums) {
        count += (num - 1) / mid;
      }
      if (count > maxOperations) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return left;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag/submissions/1472445262/){:target="_blank"}

# 설명
1. nums의 각 가방에 들어있는 공들의 갯수를 이용하여 아래의 규칙을 이용하여 maxOperations 횟수 내 나눌 수 있는 가방 별 공의 최소 갯수를 계산하는 문제이다.
- nums의 각 가방 내 값은 중복되지 않는 임의 두 갯수의 공으로 나누어 새 가방에 담는다.
- 각 수행 별 최대 갯수의 공으로 가방을 분배해야 한다.

2. left와 right는 공을 적정한 갯수로 나누기 위한 공의 갯수인 하한값과 상한 값을 저장한 값으로, 1과 1000000000으로 초기화한다.

3. left가 right미만일 때 까지 아래를 반복한다.
- mid에 $\frac{left + rigt}{2}$인 중앙값을 넣어준 후, count인 나눈 횟수를 0으로 초기화한다.
- nums내 각 값을을 순차적으로 num에 넣어 count에 ${num - 1}{mid}$ 값을 더해 mid로 나눌 경우 나눌 수 있는 갯수를 계산한다.
- count가 maxOperations보다 큰 가능 횟수를 초과하는 경우, left에 $mid + 1$을 넣어 범위를 축소시킨다.
- 위의 경우가 아니라면, rigt에 mid를 넣어 범위를 축소시킨다.

4. 반복이 완료되면 공의 최소 갯수가 저장된 left를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumLimitOfBallsInABag.java){:target="_blank"}에서 확인 가능합니다.