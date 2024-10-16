---
title: "Leetcode Java Koko Eating Bananas"
excerpt: "Leetcode Koko Eating Bananas Java"
last_modified_at: 2023-03-16T11:30:00
header:
  image: /assets/images/leetcode/koko-eating-bananas.png
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
[Link](https://leetcode.com/problems/koko-eating-bananas){:target="_blank"}

# 코드
```java
class Solution {

  public int minEatingSpeed(int[] piles, int h) {
    int left = 1;
    int right = 1000000000;
    while (left < right) {
      int mid = (left + right) / 2;
      int times = 0;
      for (int pile : piles) {
        times += (pile + mid - 1) / mid;
      }
      if (times > h) {
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
[Link](https://leetcode.com/problems/koko-eating-bananas/submissions/916326510/){:target="_blank"}

# 설명
1. 바나나의 갯수가 저장된 piles를 h 시간동안 다 먹을 수 있는 시간당 바나나의 수를 구하는 문제이다.
- 단, 시간 당 먹을 수 있는 바나나의 수가 piles에서 고른 바나나의 수보다 크다면 선택한 바나나의 갯수까지 먹고 다음 시간에 piles 내 바나나를 선택하여 먹을 수 있다.

2. left와 right는 시간 별 먹을 수 있는 바나나의 수를 탐색하기 위한 위치 변수로, 최소 갯수인 1과 최대 갯수인 1,000,000,000으로 초기화한다.

3. left가 right 미만까지 아래를 수행한다.
- mid는 left와 right의 중앙 값으로, $\frac{left + right}{2}$를 넣어준다.
- times는 piles의 값을 이용하여 시간 당 mid개를 먹을 때, 소요되는 시간을 저장한다.
- times가 h보다 큰 경우, left에 $mid + 1$을 넣어 시간 당 먹을 수 있는 바나나의 갯수를 증가시켜 범위을 좁힌다.
- times가 h보다 크지 않는 경우, right에 mid를 넣어 시간 당 먹을 수 있는 바나나의 갯수를 감소시켜 범위를 좁힌다.

4. 반복이 완료되면 piles를 h 시간동안 다 먹을 수 있는 시간당 바나나의 수를 탐색한 left를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KokoEatingBananas.java){:target="_blank"}에서 확인 가능합니다.