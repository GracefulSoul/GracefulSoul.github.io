---
title: "Leetcode Java Smallest Rotation with Highest Score"
excerpt: "Leetcode Smallest Rotation with Highest Score Java"
last_modified_at: 2023-01-10T20:50:00
header:
  image: /assets/images/leetcode/smallest-rotation-with-highest-score.png
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
[Link](https://leetcode.com/problems/smallest-rotation-with-highest-score){:target="_blank"}

# 코드
```java
class Solution {

  public int bestRotation(int[] nums) {
    int length = nums.length;
    int[] change = new int[length];
    for (int idx = 0; idx < length; idx++) {
      change[(idx - nums[idx] + 1 + length) % length]--;
    }
    int rotation = 0;
    for (int idx = 1; idx < length; idx++) {
      change[idx] += change[idx - 1] + 1;
      rotation = change[idx] > change[rotation] ? idx : rotation;
    }
    return rotation;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/smallest-rotation-with-highest-score/submissions/875413724/){:target="_blank"}

# 설명
1. nums의 각 위치에 존재하는 값이 위치 인덱스 보다 작거나 같으면 점수가 부여되는데, 이 때 가장 큰 점수가 되기 위해 nums를 좌측으로 이동해야하는 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- change는 현재 위치에 따른 점수의 손실을 저장할 변수로, length 길이로 초기화 하여 $idx - nums[idx] + 1 + length$를 length로 나눈 나머지 값에 해당하는 위치 값을 감소시켜 현재 위치에 대한 손실된 값을 계산해준다.
- rotation은 좌측으로 이동해야하는 횟수를 저장한 변수로, 0으로 초기화한다.

3. 1부터 length까지 idx를 증가시키며 아래를 수행한다.
- change의 idx번째 값에 이전 위치의 값에 1을 증가시켜준다.
- rotation에 change의 idx번째 값이 rotation번째 값보다 큰 경우 idx를, 아니면 rotation을 넣어준다.

4. 반복이 완료되면 이동 횟수가 저장된 rotation을 주어진 문제의 결과로 반환한다.

# 해설
- nums의 각 위치 idx에서 $(idx - 1 + length) % length$로 이동할 때 기본적으로 아래의 경우 중 하나를 만족해야 한다.
  - change[idx] > idx를 만족할 때, 점수를 잃지 않는다.
  - 우측인 0에서 $length - 1$로 이동하는 경우, 점수를 획득한다.
  - 좌측인 $change[idx] == idx$이면서 $idx - 1$로 이동할 때, 점수를 잃는다.
- 회전이 되는 위치인 k와 값 idx번째 위치의 관계는 $k = (idx - change[idx] + 1 + length) % length$로, idx를 반복하여 잃은 점수가 저장된 change[k]를 2번의 변수 선언 이후 계산하는 것이다.
- 3번에서 $k - 1$에서 왼쪽으로 이동하는 k단계를 계산하기 위해 $change[k] = change[k - 1] + 1$를 이용하여 각 변화된 값을 넣어 change내 idx와 rotation번째 값의 비교를 통해 최종 이동 횟수를 구한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SmallestRotationWithHighestScore.java){:target="_blank"}에서 확인 가능합니다.