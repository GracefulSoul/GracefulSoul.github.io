---
title: "Leetcode Java Hand of Straights"
excerpt: "Leetcode Hand of Straights Java"
last_modified_at: 2023-02-20T19:20:00
header:
  image: /assets/images/leetcode/hand-of-straights.png
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
[Link](https://leetcode.com/problems/hand-of-straights){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isNStraightHand(int[] hand, int groupSize) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int card : hand) {
      map.put(card, map.getOrDefault(card, 0) + 1);
    }
    Arrays.sort(hand);
    for (int card : hand) {
      if (map.get(card) <= 0) {
        continue;
      }
      for (int i = 0; i < groupSize; i++) {
        int count = map.getOrDefault(card + i, 0);
        if (count > 0) {
          map.put(card + i, count - 1);
        } else {
          return false;
        }
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/hand-of-straights/submissions/901495118/){:target="_blank"}

# 설명
1. hand의 각 숫자들을 증가하는 값으로 구성된 groupSize개의 그룹으로 구성할 수 있는지 검증하는 문제이다.

2. map에 카드 값 별 개수를 키와 값으로 모두 넣어준다.

3. hand를 오름차순으로 정렬하고, 각 값을 card에 너허 아래를 수행한다.
- map의 card번째 값이 0 이하로 모두 사용한 경우, 다음 값으로 넘어간다.
- 0부터 groupSize 미만까지 i를 증가시키며 아래를 수행한다.
  - count에 map의 $card + i$번째 카드의 개수를 넣어준다.
  - count가 0 초과라면 개수를 차감하여 다시 map에 넣어준다.
  - 위의 경우가 아니라면 그룹 분할이 불가능하므로 false를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 그룹 분할이 가능하므로 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HandOfStraights.java){:target="_blank"}에서 확인 가능합니다.