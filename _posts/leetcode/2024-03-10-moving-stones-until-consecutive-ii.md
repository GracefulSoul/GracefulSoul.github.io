---
title: "Leetcode Java Moving Stones Until Consecutive II"
excerpt: "Leetcode Moving Stones Until Consecutive II Java"
last_modified_at: 2024-03-10T11:30:00
header:
  image: /assets/images/leetcode/moving-stones-until-consecutive-ii.png
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
[Link](https://leetcode.com/problems/moving-stones-until-consecutive-ii){:target="_blank"}

# 코드
```java
class Solution {

  public int[] numMovesStonesII(int[] stones) {
    Arrays.sort(stones);
    int length = stones.length;
    int low = length;
    int high = Math.max(stones[length - 1] - stones[1], stones[length - 2] - stones[0]) - length + 2;
    for (int i = 0, j = 0; j < length; j++) {
      while (stones[j] - stones[i] >= length) {
        i++;
      }
      if (j - i + 1 == length - 1 && stones[j] - stones[i] == length - 2) {
        low = Math.min(low, 2);
      } else {
        low = Math.min(low, length - (j - i + 1));
      }
    }
    return new int[] { low, high };
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-common-value/submissions/1198052970/){:target="_blank"}

# 설명
1. 돌의 위치가 저장된 stones의 값들을 이용하여 아래의 규칙대로 게임을 수행할 때, 최소 이동 횟수와 최대 이동 횟수를 구하여 정수 배열로 반환하는 문제이다.
- 위치가 가장 작거나 큰 돌을 엔드포인트 돌이라고 하고, 비어 있는 값으로 바꾸면 더 이상 엔드포인트 돌이 아니게된다.
  - 엔드포인트 돌을 변경할 때, 가장 작거나 큰 값으로 변경해야하면 이동할 수 없다.
- 더 이상 돌의 위치를 변경할 수 없을 때 게임은 종료된다.

2. stones의 값들을 오름차순 정렬해준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- length는 stones의 길이를 저장한 변수이다.
- low는 최소 이동 횟수를 저장할 변수로, 최대 변경 가능한 length로 초기화한다.
- high는 최대 이동 횟수를 저장할 변수로, $stones[length - 1] - stones[1]$의 값과 $stones[length - 2] - stones[0]$의 값 중 큰 값에 $length - 2$를 뺀 값을 넣어준다.
  - 가장 작은 값의 돌을 유지한 채 이동할 수 있는 최대 이동 횟수는, $(stones[length - 1] - stones[length - 2] - 1) + (stones[length - 2] - stones[length - 3] - 1) + ... + (stones[2] - stones[1] - 1) = stones[n - 1] - stones[1] - (length - 2)$이다.
  - 가장 큰 값의 돌을 유지한 채 이동할 수 있는 최대 이동 횟수는, 위와 동일하게 계산하여 $stones[length - 2] - stones[0] - (length - 2)$를 만족한다.
  - 위의 경우를 대입하여 $stones[n - 1] - stones[1]$의 값과 $stones[length - 2] - stones[0]$의 값 중 큰 값에 $length - 2$를 빼준 값이 최대 이동 횟수가 된다.

4. i와 j가 0부터 j가 length 미만일 때 까지 j를 증가시키며 아래를 수행한다.
- $stones[j] - stones[i]$의 값이 length보다 큰 경우, i를 증가시켜 위치를 증가시켜준다.
- $j - i + 1$의 값이 $length - 1$과 동일하고 $stones[j] - stones[i]$의 값이 $length - 2$와 동일한지 검증하여 아래를 수행한다.
  - 동일한 경우, low에 low와 2 중 작은 값을 넣어준다.
  - 동일하지 않은 경우, low에 low와 $length - (j - i + 1)$ 중 작은 값을 넣어준다.

5. 반복이 완료되면 low와 high를 정수 배열에 순차적으로 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MovingStonesUntilConsecutiveII.java){:target="_blank"}에서 확인 가능합니다.