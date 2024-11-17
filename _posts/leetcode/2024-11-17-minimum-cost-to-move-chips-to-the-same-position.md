---
title: "Leetcode Java Minimum Cost to Move Chips to The Same Position"
excerpt: "Leetcode - 'Minimum Cost to Move Chips to The Same Position' 문제 Java 풀이"
last_modified_at: 2024-11-17T09:30:00
header:
  image: /assets/images/leetcode/minimum-cost-to-move-chips-to-the-same-position.png
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
[Link](https://leetcode.com/problems/minimum-cost-to-move-chips-to-the-same-position/){:target="_blank"}

# 코드
```java
class Solution {

  public int minCostToMoveChips(int[] position) {
    int[] count = new int[2];
    for (int p : position) {
      count[p % 2]++;
    }
    return Math.min(count[0], count[1]);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-cost-to-move-chips-to-the-same-position/submissions/1454749017/){:target="_blank"}

# 설명
1. position에 있는 각 코인들을 아래의 규칙대로 하나의 위치에 모으기 위한 비용을 계산하는 문제이다.
- 현재 위치에서 2 칸을 앞뒤로 움직이는 경우, 비용을 0으로 계산한다.
- 현재 위치에서 1 칸을 앞뒤로 움직이는 경우, 비용을 1로 계산한다.

2. count는 홀수와 짝수 위치를 계산하기 위한 변수로, 2 크기의 정수 배열로 초기화한다.

3. position의 각 값을 순차적으로 짝수인지 홀수인지에 따라 count에 값을 넣어준다.

4. 반복이 완료되면 짝수의 위치인 count[0]의 값과 홀수의 위치인 count[1]의 값 중 작은 값을 주어진 문제의 결과로 반환한다.

# 해설
- 위치의 값이 짝수인 값이 많은 경우, 짝수의 임의 한 지점 위치의 값을 앞뒤 인접한 위치까지 2칸 씩 비용 0으로 모아 홀수인 갯수만큼 이동시키면 된다.
- 위치의 값이 홀수인 값이 많은 경우, 홀수의 임의 한 지점 위치의 값을 앞뒤 인접한 위치까지 2칸 씩 비용 0으로 모아 짝수인 갯수만큼 이동시키면 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumCostToMoveChipsToTheSamePosition.java){:target="_blank"}에서 확인 가능합니다.