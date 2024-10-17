---
title: "Leetcode Java Prison Cells After N Days"
excerpt: "Leetcode Medium - 'Prison Cells After N Days' 문제 Java 풀이"
last_modified_at: 2023-07-24T19:40:00
header:
  image: /assets/images/leetcode/prison-cells-after-n-days.png
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
[Link](https://leetcode.com/problems/prison-cells-after-n-days){:target="_blank"}

# 코드
```java
class Solution {

  public int[] prisonAfterNDays(int[] cells, int n) {
    for (n = ((n - 1) % 14) + 1; n > 0; n--) {
      int[] temp = new int[8];
      for (int i = 1; i < 7; i++) {
        temp[i] = cells[i - 1] == cells[i + 1] ? 1 : 0;
      }
      cells = temp;
    }
    return cells;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/prison-cells-after-n-days/submissions/1002511386/){:target="_blank"}

# 설명
1. 8칸의 cells를 아래의 규칙대로 n번 수행하였을 때 결과를 반환하는 문제이다.
- cells 내 각 셀의 좌측과 우측 위치의 값이 같은 경우, 다음 수행의 해당 위치 값은 1로 채워진다.
- 위의 경우가 아니라면 0으로 값이 채워진다.
- 첫 셀과 마지막 셀은 첫 수행 이후로는 0으로 채워진다.

2. $n - 1$을 14로 나눈 나머지 값에 1을 더한 값부터 0 이상일 때 까지 n을 감소시키며 아래를 수행한다.
- temp는 규칙을 수행한 다음 값을 넣어줄 변수로, cells와 동일한 8 크기의 정수 배열로 초기화한다.
- 1부터 7 미만까지 i를 증가시키며 cells의 각 위치 별 전후 값이 동일하면 1을, 아니면 0을 넣어준다.
- cells에 temp를 넣어준다.

3. 반복이 완료되면 규칙대로 수행한 결과인 cells를 주어진 문제의 결과로 반환한다.

# 해설
- cells가 [0, 1, 0, 1, 1, 0, 0, 1]일때, 기본 규칙대로 계속 반복하면 아래와 같다.
```
1: [0, 1, 1, 0, 0, 0, 0, 0]
2: [0, 0, 0, 0, 1, 1, 1, 0]
... 중략 ...
6: [0, 0, 1, 0, 1, 1, 0, 0]
7: [0, 0, 1, 1, 0, 0, 0, 0]
8: [0, 0, 0, 0, 0, 1, 1, 0]
... 중략 ...
14: [0, 0, 0, 0, 1, 1, 0, 0]
15: [0, 1, 1, 0, 0, 0, 0, 0]
```
- 이 결과를 통해 1, 14번 수행한 결과가 동일한 결과가 나오는 것을 알 수 있다.
- 이 패턴을 파악하였으므로 이용하여 n번 반복하는 것이 아니라 $n - 1$을 14로 나눈 나머지 값에 1을 더한 값만큼 반복하여 수행한 배열이 주어진 문제의 결과임을 유추할 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PrisonCellsAfterNDays.java){:target="_blank"}에서 확인 가능합니다.