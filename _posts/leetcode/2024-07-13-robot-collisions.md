---
title: "Leetcode Java Robot Collisions"
excerpt: "Leetcode Hard - 'Robot Collisions' 문제 Java 풀이"
last_modified_at: 2024-07-13T13:40:00
header:
  image: /assets/images/leetcode/robot-collisions.png
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
[Link](https://leetcode.com/problems/robot-collisions/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> survivedRobotsHealths(int[] positions, int[] healths, String directions) {
    int length = positions.length;
    Integer[] indices = new Integer[length];
    for (int i = 0; i < length; i++) {
      indices[i] = i;
    }
    Arrays.sort(indices, (l, r) -> Integer.compare(positions[l], positions[r]));
    List<Integer> result = new ArrayList<>();
    Stack<Integer> stack = new Stack<>();
    for (int curr : indices) {
      if (directions.charAt(curr) == 'R') {
        stack.push(curr);
      } else {
        while (!stack.isEmpty() && healths[curr] > 0) {
          int top = stack.pop();
          if (healths[top] > healths[curr]) {
            healths[top] -= 1;
            healths[curr] = 0;
            stack.push(top);
          } else if (healths[top] < healths[curr]) {
            healths[curr] -= 1;
            healths[top] = 0;
          } else {
            healths[curr] = 0;
            healths[top] = 0;
          }
        }
      }
    }
    for (int health : healths) {
      if (health > 0) {
        result.add(health);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/robot-collisions/submissions/1319298462/){:target="_blank"}

# 설명
1. 직선 상 로봇의 각 위치를 나타내는 positions과 체력을 나타내는 healths을 이용하여 directions로 각각 이동을 할 때, 남아있는 로봇의 상태를 반환하는 문제이다.
- 두 로봇이 충돌하면 체력이 높은 로봇이 살아남으며, 살아남은 로봇의 체력은 1 차감된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 로봇의 수를 저장할 변수로, positions의 길이로 초기화한다.
- indices는 로봇의 위치를 저장할 변수로, length까지 각 값을 넣어주고 positions를 이용하여 로봇의 상대적 위치를 순서대로 넣어준다.
- result는 남아있는 로봇의 상태를 저장할 변수로, ArrayList로 초기화한다.
- stack은 로봇의 이동에 사용될 변수로, Stack으로 초기화한다.

3. indices를 순차적으로 curr에 넣어 아래를 수행한다.
- directions의 curr번째 문자가 'R'인 우측으로 이동하는 경우, stack에 curr을 넣어준다.
- directions의 curr번째 문자가 'L'인 좌측으로 이동하는 경우, stack이 비어있지 않고 healths[curr]의 값이 0 초과일 때 까지 아래를 반복한다.
  - top에 stack에서 로봇 위치 값을 넣어준다.
  - healths[top]의 값이 healths[curr]의 값보다 크면 top번째 로봇이 살아남으므로, healths[top]의 값을 감소시키고 healths[curr]의 위치에 0을 넣어준 후 stack에 다시 top을 넣어준다.
  - healths[top]의 값이 healths[curr]의 값보다 작으면 curr번째 로봇이 살아남으므로, healths[curr]의 값을 감소시키고 healths[top]의 위치에 0을 넣어준다.
  - healths[top]의 값이 healths[curr]의 값과 같으면 두 로봇은 같이 죽으므로, healths의 두 위치 값에 0을 넣어준다.

4. healths의 각 값을 순차적으로 반복하여 0 초과인 경우에 result에 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RobotCollisions.java){:target="_blank"}에서 확인 가능합니다.