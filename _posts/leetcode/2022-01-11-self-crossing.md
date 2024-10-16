---
title: "Leetcode Java Self Crossing"
excerpt: "Leetcode Self Crossing Java 풀이"
last_modified_at: 2022-01-11T20:00:00
header:
  image: /assets/images/leetcode/self-crossing.png
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
[Link](https://leetcode.com/problems/self-crossing/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isSelfCrossing(int[] distance) {
    int length = distance.length;
    if (length <= 3) {
      return false;
    }
    int idx = 2;
    while (idx < length && distance[idx] > distance[idx - 2]) {
      idx++;
    }
    if (idx >= length) {
      return false;
    }
    if ((idx >= 4 && distance[idx] >= distance[idx - 2] - distance[idx - 4]) ||
      (idx == 3 && distance[idx] == distance[idx - 2])) {
      distance[idx - 1] -= distance[idx - 3];
    }
    idx++;
    while (idx < length) {
      if (distance[idx] >= distance[idx - 2]) {
        return true;
      }
      idx++;
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/617572069/){:target="_blank"}

# 설명
1. 주어진 정수 배열 distance를 이용하여 [0, 0]부터 시작하여 상, 좌, 하, 우 순서로 이동하여 교차하는 지점이 있는지 검증하는 문제이다.

2. length는 distance의 길이를 저장할 변수로, distance.length로 초기화 시켜준다.

3. length가 3 이하인 경우, 교차하는 구간이 존재하지 않기 때문에, false를 주어진 문제의 결과로 반환한다.
- 대각선을 제외한 줄을 그어 교차하는 구간을 구하기 위해선, 최소 4번의 이동이 필요하다.

4. idx에 2를 넣고, idx가 length보다 작고 distance의 idx번째 값이 distance의 $idx - 2$번째 값보다 클 때 까지 idx를 증가시킨다.

5. idx가 length와 같거나 클 경우 교차하는 구간이 존재하지 않으므로, false를 주어진 문제의 결과로 반환한다.
- 4번을 통해 선의 이동이 소용돌이처럼 교차하지 않고 커지는 경우이다.

6. 아래의 조건들 중 하나라도 만족하면, distance의 $idx - 1$번째 값에 distance의 $idx - 3$번째 값이 차이를 distance의 $idx - 1$번째 자리에 넣어 바깥쪽으로 나선형 모양이 되는 것을 안쪽으로 전환시킨다.
- idx가 4보다 클 때, distance의 idx번째 값이 distance의 $idx - 2$번째 값과 distinct의 $idx - 4$번째 값의 차이보다 크거나 같은 경우.
- idx가 3인 경우, distance의 idx번째 값과 distance의 $idx - 2$번째 값이 같은 경우.

7. idx를 증가시키고, idx가 length보다 작을 때까지 아래를 반복한다.
- distance의 idx번째 값이 distance의 $idx - 2$번쨰 값보다 크거나 같으면 교차하는 지점이 생긴다는 의미이므로, true를 주어진 문제의 결과로 반환한다.
- idx를 증가시키고 반복을 계속 수행한다.

8. 반복이 종료되면 교차하는 지점이 생기지 않는다는 의미이므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SelfCrossing.java){:target="_blank"}에서 확인 가능합니다.