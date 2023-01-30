---
title: "Leetcode Java Card Flipping Game"
excerpt: "Leetcode Card Flipping Game Java"
last_modified_at: 2023-01-30T20:00:00
header:
  image: /assets/images/leetcode/card-flipping-game.png
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
[Link](https://leetcode.com/problems/card-flipping-game){:target="_blank"}

# 코드
```java
class Solution {

  public int flipgame(int[] fronts, int[] backs) {
    Set<Integer> set = new HashSet<>();
    for (int idx = 0; idx < fronts.length; idx++) {
      if (fronts[idx] == backs[idx]) {
        set.add(fronts[idx]);
      } 
    }
    int result = 2001;
    for (int idx = 0; idx < fronts.length; idx++) {
      if (!set.contains(backs[idx])) {
        result = Math.min(result, backs[idx]);
      }
      if (!set.contains(fronts[idx])) {
        result = Math.min(result, fronts[idx]);
      }
    }
    return result % 2001;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/card-flipping-game/submissions/888055254/){:target="_blank"}

# 설명
1. 카드들의 앞면의 숫자인 fronts와 뒷면의 숫자인 backs를 이용하여 카드를 뒤집었을 경우, 가능한 최소 크기의 좋은 정수를 반환하는 문제이다.
- 앞면과 뒷면의 숫자가 동일한 경우, 값의 변화가 없으므로 좋은 정수가 될 수 없다.
- 좋은 정수가 없을 경우, 0을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- set은 앞면과 뒤면의 숫자가 동일한 숫자를 저장할 변수로, fronts와 backs 내 동일한 숫자를 넣어준다.
- result는 최소 가능한 좋은 정수를 저장할 변수로, 숫자의 최대 크기인 2000보다 큰 2001로 초기화한다.

3. 0부터 fronts의 길이 미만까지 idx를 증가시키며 아래를 수행한다.
- set에 backs의 idx번째 값이 없는 경우, result에 해당 값과 backs의 idx번째 값 중 작은 값을 넣어준다.
- set에 fronts의 idx번째 값이 없는 경우, result에 해당 값과 fronts의 idx번째 값 중 작은 값을 넣어준다.

4. 반복이 완료되면 result를 2001로 나눈 나머지 값을 주어진 문제의 결과로 반환한다.

3. 

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CardFlippingGame.java){:target="_blank"}에서 확인 가능합니다.