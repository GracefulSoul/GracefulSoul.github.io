---
title: "Leetcode Java Maximum Length of Pair Chain"
excerpt: "Leetcode Maximum Length of Pair Chain Java"
last_modified_at: 2022-09-03T09:30:00
header:
  image: /assets/images/leetcode/maximum-length-of-pair-chain.png
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
[Link](https://leetcode.com/problems/maximum-length-of-pair-chain/){:target="_blank"}

# 코드
```java
class Solution {

  public int findLongestChain(int[][] pairs) {
    Arrays.sort(pairs, (a, b) -> a[0] - b[0]);
    int pre = pairs[0][1];
    int count = 1;
    for (int idx = 1; idx < pairs.length; idx++) {
      if (pairs[idx][0] > pre) {
        pre = pairs[idx][1];
        count++;
      } else {
        pre = Math.min(pre, pairs[idx][1]);
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/790017249/){:target="_blank"}

# 설명
1. pairs 내 아래의 조건으로 연결 할 경우, 최대 길이를 구하는 문제이다.
- pairs[i] = [left<sub>i</sub>, right<sub>i</sub>], left<sub>i</sub> < right<sub>i</sub>
- p1 = [a, b]이고 p2 = [c, d]일 때, b < c을 만족하는 경우 연결이 가능하다.

2. pairs의 모든 배열들을 배열 내 첫 번째 값의 오름차순으로 정렬한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- pre는 연결된 이전 배열의 두 번째 값을 저장할 변수로, pairs의 첫 배열의 두 번째 값으로 초기화한다.
- count는 연결 쌍의 최대 길이를 계산할 변수로, 위의 첫 배열이 포함되었으므로 1로 초기화한다.

4. 첫 값이 포함되었으므로, 1부터 pairs의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- pairs[idx][0]의 값이 pre보다 큰 경우 연결이 가능하므로, pre에 pairs[idx][1] 값을 넣어주고 count를 증가시킨다.
- 그 외의 경우 pre에 pre와 paris[idx][1] 중 작은 값을 넣어준다.

5. 반복이 완료되면 계산된 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumLengthOfPairChain.java){:target="_blank"}에서 확인 가능합니다.