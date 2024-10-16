---
title: "Leetcode Java Range Addition II"
excerpt: "Leetcode Range Addition II Java"
last_modified_at: 2022-07-27T19:00:00
header:
  image: /assets/images/leetcode/range-addition-ii.png
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
[Link](https://leetcode.com/problems/range-addition-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxCount(int m, int n, int[][] ops) {
    for (int[] op : ops) {
      m = Math.min(m, op[0]);
      n = Math.min(n, op[1]);
    }
    return m * n;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/758005431/){:target="_blank"}

# 설명
1. $m \times n$ 크기의 행렬의 모든 값을 0으로 초기화한 M이 주어지면, 아래의 조건을 만족하는 최대 정수의 수를 반환하는 문제이다.
- ops[i] = [a<sub>i</sub>, b<sub>i</sub>]일 때, 0 <= x < a<sub>i</sub> 및 0 <= y < b<sub>i</sub>에 대해 M[x][y]를 1씩 증가해야한다.

2. ops를 반복하여 아래를 수행한다.
- m에 m과 op[0]의 값 중 작은 값을 넣어준다.
- n에 n과 op[1]의 값 중 작은 값을 넣어준다.

3. 반복이 완료되면 $m \times n$의 결과를 주어진 문제의 결과로 반환한다.
- 최소 범위의 m과 n은 주어진 조건을 수행한 이후, 최댓 값이 되기 때문에 해당 결과가 주어진 문제의 결과가 되는 것이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RangeAdditionII.java){:target="_blank"}에서 확인 가능합니다.