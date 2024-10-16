---
title: "Leetcode Java Can Place Flowers"
excerpt: "Leetcode Can Place Flowers Java"
last_modified_at: 2022-07-31T09:00:00
header:
  image: /assets/images/leetcode/can-place-flowers.png
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
[Link](https://leetcode.com/problems/can-place-flowers/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canPlaceFlowers(int[] flowerbed, int n) {
    if (n == 0) {
      return true;
    }
    int pre = -1;
    for (int idx = 0; idx < flowerbed.length; idx++) {
      if (flowerbed[idx] == 0 &&
          (pre < idx - 1 || idx == 0) &&
          (idx + 1 == flowerbed.length || flowerbed[idx + 1] == 0)) {
        n--;
        if (n == 0) {
          return true;
        }
        pre = idx;
      } else if (flowerbed[idx] == 1) {
        pre = idx;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/761006010/){:target="_blank"}

# 설명
1. 화단인 flowerbed에 n개의 꽃을 한 칸 건너 한 칸마다 심는 것이 가능한지 검증하는 문제이다.

2. 꽃을 꽃의 수인 n이 0인 경우, 무조건 만족하므로 true를 주어진 문제의 결과로 반환한다.

3. 이전 꽃의 위치 값을 저장하기 위한 pre를 -1로 초기화한다.

4. 0부터 flowerbed의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- flowerbed의 idx번째 값이 0이고, idx가 0이거나 pre가 $idx - 1$보다 작고, idx가 마지막 값 이전 위치거나 flowerbed의 마지막 값이 0인 경우 아래를 수행한다.
  - n을 감소시키고, n이 0인 경우 꽃을 다 꽃았으면 true를 주어진 문제의 결과로 반환한다.
  - pre에 idx를 넣어 꽃의 위치를 갱신해준다.
- flowerbed의 idx번째 값이 1인 경우, pre에 idx를 넣어 꽃의 위치를 갱신해준다.

5. 반복이 완료되면 꽃을 다 꽃지 못한 경우이므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CanPlaceFlowers.java){:target="_blank"}에서 확인 가능합니다.