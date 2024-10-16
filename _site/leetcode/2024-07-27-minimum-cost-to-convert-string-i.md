---
title: "Leetcode Java Minimum Cost to Convert String I"
excerpt: "Leetcode Minimum Cost to Convert String I Java"
last_modified_at: 2024-07-27T09:20:00
header:
  image: /assets/images/leetcode/minimum-cost-to-convert-string-i.png
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
[Link](https://leetcode.com/problems/minimum-cost-to-convert-string-i/){:target="_blank"}

# 코드
```java
class Solution {

  public long minimumCost(String source, String target, char[] original, char[] changed, int[] cost) {
    long result = 0;
    long[][] costs = new long[26][26];
    for (long[] row : costs) {
      Arrays.fill(row, Integer.MAX_VALUE);
    }
    for (int i = 0; i < original.length; i++) {
      int num1 = original[i] - 'a';
      int num2 = changed[i] - 'a';
      costs[num1][num2] = Math.min(costs[num1][num2], cost[i]);
    }
    for (int i = 0; i < 26; i++) {
      costs[i][i] = 0;
    }
    for (int k = 0; k < 26; k++) {
      for (int i = 0; i < 26; i++) {
        for (int j = 0; j < 26; j++) {
          costs[i][j] = Math.min(costs[i][j], costs[i][k] + costs[k][j]);
        }
      }
    }
    for (int i = 0; i < source.length(); i++) {
      int num1 = source.charAt(i) - 'a';
      int num2 = target.charAt(i) - 'a';
      if (num1 == num2) {
        continue;
      }
      if (costs[num1][num2] == Integer.MAX_VALUE) {
        return -1L;
      } else {
        result += costs[num1][num2];
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-cost-to-convert-string-i/submissions/1334595601/){:target="_blank"}

# 설명
1. source 문자열을 target 문자열로 변경할 때 발생하는 최소 비용을 계산하는 문제이다.
- original[i] 문자를 changed[i] 문자로 바꿀 때 발생하는 비용은 cost[i] 이다.
- source 문자열을 target 문자열로 변경이 불가능한 경우, -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장하기 위한 변수로, 0으로 초기화한다.
- costs [Floyd Warshall](https://en.wikipedia.org/wiki/Floyd%E2%80%93Warshall_algorithm){:target="_blank"} 알고리즘을 이용하여 거리를 계산하기 위한 변수로, 문자열의 갯수인 26을 이용하여 $26 \times 26$ 크기의 2차원 정수 배열로 초기화 후 아래를 수행한다.
  - costs의 모든 위치에 정수의 최댓값을 넣어준다.
  - original과 changed를 costs의 위치에 현재 값과 cost 값 중 작은 값을 넣어준다.
  - 자기 자신의 값을 변경하는 경우의 위치에는 값을 0으로 초기화해준다.
  - 값을 여러 번 바꿔 비용이 발생하는 경우를 위해서 costs[i][j]에 기존 비용인 자기 자신의 값과 k번째 문자를 거쳐 바꿔지는 경우인 $costs[i][k] + costs[k][j]$ 중 최소 비용을 넣어준다.

3. 0부터 26 미만까지 i를 증가시키면서 아래를 반복한다.
- source의 i번째 문자가 target의 i번째 문자와 동일하면 바꿀 필요가 없으므로, 다음 반복을 수행한다.
- costs의 source의 i번째 문자 순서와 target의 i번째 문자 순서의 값이 동일하여 변경이 불가능한 경우, -1을 주어진 문제의 결과로 반환한다.
- costs의 source의 i번째 문자 순서와 target의 i번째 문자 순서의 값이 동일하여 변경이 가능한 경우, result에 해당 값을 더해준다.

4. 반복이 완료되면 최소 비용인 result를 주어진 문제의 결과로 반환한다.

# 해설
- 여느 문제와 같이 도시의 숫자가 작은 값부터 이동 가능한 도시의 갯수가 동일한 경우를 포함하는 이유는, 문제의 조건인 도시의 숫자가 큰 경우만 남기기 위함이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumCostToConvertStringI.java){:target="_blank"}에서 확인 가능합니다.