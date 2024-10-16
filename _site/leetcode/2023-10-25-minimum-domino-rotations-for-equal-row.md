---
title: "Leetcode Java Minimum Domino Rotations For Equal Row"
excerpt: "Leetcode Minimum Domino Rotations For Equal Row Java"
last_modified_at: 2023-10-25T20:30:00
header:
  image: /assets/images/leetcode/minimum-domino-rotations-for-equal-row.png
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
[Link](https://leetcode.com/problems/minimum-domino-rotations-for-equal-row){:target="_blank"}

# 코드
```java
class Solution {

  public int minDominoRotations(int[] tops, int[] bottoms) {
    int result = -1;
    for (int i = 1; i <= 6; i++) {
      int curr = this.calculate(tops, bottoms, i);
      if (curr != -1 && (result == -1 || result > curr)) {
        result = curr;
      }
    }
    return result;
  }

  private int calculate(int[] tops, int[] bottoms, int index) {
    int top = 0;
    int bottom = 0;
    for (int i = 0; i < tops.length; i++) {
      if (tops[i] != index && bottoms[i] != index) {
        return -1;
      } else if (tops[i] != index) {
        top++;
      } else if (bottoms[i] != index) {
        bottom++;
      }
    }
    return Math.min(top, bottom);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-domino-rotations-for-equal-row/submissions/1083791277/){:target="_blank"}

# 설명
1. tops와 bottoms의 두 배열 내 한 배열 내 값들이 동일하게 만들기 위한 최소 횟수를 구하는 문제이다.
- 단, 한 배열이라도 동일하게 만들 수 없으면 -1을 주어진 문제의 결과로 반환한다.

2. result는 최소 횟수를 저장하기 위한 변수로, -1로 초기화한다.

3. 배열 내 값의 범위인 1부터 6까지 i를 증가시키며 아래를 반복한다.
- curr에 4번에서 정의한 calculate(int[] tops, int[] bottoms, int index) 메서드를 수행한 결과를 넣어준다.
- curr이 -1이면서 result가 -1이거나 curr보다 큰 경우, result에 curr을 넣어준다.

4. 현재 위치까지 top과 bottom의 바꾼 최소 갯수를 계산할 calculate(int[] tops, int[] bottoms, int index) 메서드를 정의한다.
- 변경 횟수를 저장할 top과 bottom을 0으로 초기화한다.
- 0부터 top의 길이 미만까지 i를 증가시키며 아래를 반복한다.
  - tops[i]의 값과 bottom[i]의 값이 index가 아닌 경우, 동일한 값이 아니므로 -1을 반환한다.
  - tops[i]의 값만 index가 아닌 경우, top을 증가시켜 bottom의 값과 위치를 바꾼 횟수를 증가시킨다.
  - bottoms[i]의 값만 index가 아닌 경우, bottom을 증가시켜 top의 값과 위치를 바꾼 횟수를 증가시킨다.
- 반복이 완료되면 최소 변경 횟수인 top과 bottom 중 작은 값을 반환한다.

5. 3번의 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumDominoRotationsForEqualRow.java){:target="_blank"}에서 확인 가능합니다.