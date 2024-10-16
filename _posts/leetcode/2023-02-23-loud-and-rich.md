---
title: "Leetcode Java Loud and Rich"
excerpt: "Leetcode Loud and Rich Java"
last_modified_at: 2023-02-23T21:00:00
header:
  image: /assets/images/leetcode/loud-and-rich.png
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
[Link](https://leetcode.com/problems/loud-and-rich){:target="_blank"}

# 코드
```java
class Solution {

  public int[] loudAndRich(int[][] richer, int[] quiet) {
    int[] result = new int[quiet.length];
    for (int i = 0; i < quiet.length; i++) {
      result[i] = i;
    }
    while (true) {
      boolean change = false;
      for (int[] rich : richer) {
        if (quiet[result[rich[0]]] < quiet[result[rich[1]]]) {
          result[rich[1]] = result[rich[0]];
          change = true;
        }
      }
      if (!change) {
        break;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/loud-and-rich/submissions/903510331/){:target="_blank"}

# 설명
1. [0, $n - 1$]까지 7명의 그룹이 존재하는 richer를 이용하여 아래를 만족하는 사람들의 배열을 반환하는 문제이다.
- richer[i] = [a<sub>i</sub>, b<sub>i</sub>]일 때, b<sub>i</sub>보다 a<sub>i</sub>가 더 많은 돈을 가지고 있다는 의미이다.
- quiet는 i번째 사람의 정숙함의 정도를 나타낸다.
- answer[x] = y일 때, x보다 같거나 더 많은 돈을 가진 사람들 중에 quiet[y]의 값이 가장 작은 사람 y를 의미한다.

2. result는 결과를 저장할 배열로, quiet의 길이 크기의 정수 배열로 초기화하고 각 위치에 배열의 위치 값을 넣어준다.

3. 아래의 반복을 계속 수행한다.
- change는 변경되었는지 여부를 저장할 변수로, false로 초기화한다.
- richer의 값을 rich에 순서대로 넣어 아래를 수행한다.
  - result 내 rich의 돈 많은 사람인 첫 번째 순서에 해당하는 위치 값인 result[rich[0]]의 조용함 정도가 보다 적은 돈을 가진 사람인 두 번째 순서에 해당하는 위치 값인 result[rich[1]]의 조용함 정도보다 작은 경우, result[rich[1]]에 result[rich[0]]의 값을 넣어준다.
  - 변경 이력이 있으므로 change를 true로 바꾸어준다.
- 변경 이력이 없는 change가 false인 경우, 조건에 맞는 사람의 번호가 result에 저장되었으므로 반복을 종료한다.

4. 반복이 종료되면 조건을 만족하는 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LoudAndRich.java){:target="_blank"}에서 확인 가능합니다.