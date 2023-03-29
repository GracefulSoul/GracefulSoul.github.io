---
title: "Leetcode Java Fair Candy Swap"
excerpt: "Leetcode Fair Candy Swap Java"
last_modified_at: 2023-03-29T20:50:00
header:
  image: /assets/images/leetcode/fair-candy-swap.png
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
[Link](https://leetcode.com/problems/fair-candy-swap){:target="_blank"}

# 코드
```java
class Solution {

  public int[] fairCandySwap(int[] aliceSizes, int[] bobSizes) {
    int diff = 0;
    Set<Integer> set = new HashSet<>();
    for (int aliceSize : aliceSizes) {
      diff += aliceSize;
      set.add(aliceSize);
    }
    for (int bobSize : bobSizes) {
      diff -= bobSize;
    }
    diff /= 2;
    for (int bobSize : bobSizes) {
      if (set.contains(bobSize + diff)) {
        return new int[] { bobSize + diff, bobSize };
      }
    }
    return new int[0];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/fair-candy-swap/submissions/924189673/){:target="_blank"}

# 설명
1. 엘리스와 밥이 가진 사탕 상자 내 들어있는 사탕의 수인 aliceSizes와 bobSizes를 이용하여 서로 사탕 상자를 교환하여 사탕의 총량이 같아지기 위한 엘리스와 밥의 교환할 상자에 담긴 사탕의 수를 배열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- diff는 엘리스의 사탕과 밥의 사탕의 갯수 차이를 저장할 변수로, 0으로 초기화한다.
- set은 엘리스가 가진 사탕 상자의 갯수를 저장할 변수로, 중복을 배제하여 저장하기 위해 HashSet으로 초기화한다.

3. aliceSizes를 반복하여 diff에 엘리스가 가진 사탕 갯수를 더하고, set에는 각 사탕의 갯수를 저장해준다.

4. bobSizes를 반복하여 diff의 밥이 가진 사탕 갯수를 빼주고, diff의 값을 반으로 나누어 저장한다.

5. bobSizes의 상자 별 사탕의 수를 bobSize에 넣어 아래를 반복한다.
- 엘리스가 가진 사탕의 수가 저장된 set 내 $bobSize + diff$ 값이 존재한다면, [$bobSize + diff$, bobSize]를 주어진 문제의 결과로 반환한다.

6. 적어도 한 가지의 정답이 있으므로, 반복이 완료되면 임의의 결과를 반환한다.

# 풀이
- 엘리스가 가진 사탕의 수와 밥이 가진 사탕의 수가 동일하기 위해선 아래의 공식이 성립한다.
  - $aliceCandies - aliceSizes[i] + bobSizes[j] = bobCandies - bobSizes[j] + aliceSizes[i]$
- 위 공식을 정리하면 아래가 성립한다.
  - $aliceCandies - bobCandies = 2 \times (aliceSizes[i] - bobSizes[j])$
  - $aliceSizes[i] - bobSizes[j] = \frac{aliceCandies - bobCandies}{2}$
- 이를 이용하여 두 상자의 사탕 차이는 엘리스가 가진 사탕의 수에서 밥이 가진 사탕의 수를 뺀 절반이 된다.
- 해당 공식을 이용하여 $diff = \frac{aliceCandies - bobCandies}{2}$일 때, $diff + bobSizes[j] = aliceSizes[i]$가 성립하게 된다.
- 위를 이용하여 밥이 가진 사탕의 수에 diff을 더한 값이 엘리스가 가진 사탕의 수에 존재하면, 해당 값을 주어진 문제의 결과로 반환하는 것이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FairCandySwap.java){:target="_blank"}에서 확인 가능합니다.