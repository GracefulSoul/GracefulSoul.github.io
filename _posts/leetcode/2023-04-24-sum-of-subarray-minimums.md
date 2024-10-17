---
title: "Leetcode Java Sum of Subarray Minimums"
excerpt: "Leetcode - 'Sum of Subarray Minimums' 문제 Java 풀이"
last_modified_at: 2023-04-24T19:50:00
header:
  image: /assets/images/leetcode/sum-of-subarray-minimums.png
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
[Link](https://leetcode.com/problems/sum-of-subarray-minimums){:target="_blank"}

# 코드
```java
class Solution {

  public int sumSubarrayMins(int[] arr) {
    int length = arr.length;
    int index = 0;
    int[] dp = new int[length];
    int[] stack = new int[length + 1];
    long result = dp[0] = arr[0];
    for (int i = 1; i < length; i++) {
      while (index >= 0 && arr[stack[index]] >= arr[i]) {
        index--;
      }
      dp[i] = index < 0 ? arr[i] * (i + 1) : dp[stack[index]] + arr[i] * (i - stack[index]);
      result += dp[i];
      stack[++index] = i;
    }
    return (int) (result % 1000000007);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sum-of-subarray-minimums/submissions/938899467/){:target="_blank"}

# 설명
1. arr의 연속된 값들로 이루어진 모든 경우의 부분 배열 내 최소값 합을 계산하는 문제이다.
- 값이 매우 클 수 있으므로 모듈러 $10^9 +7$로 결과를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- index는 부분 배열을 산정하기 위한 위치를 계산할 변수로, 0으로 초기화한다.
- dp는 i번째 값까지 최소값 합을 저장할 변수로, length 크기의 정수 배열로 초기화하고 첫 값에 arr의 첫 값을 넣어준다.
- stack은 이전까지 계산한 위치 값을 저장할 변수로, $length + 1$ 크기의 정수 배열로 초기화한다.
- result는 최소값 합을 계산하기 위한 변수로, arr의 첫 값을 넣어준다.

3. 1부터 length 미만까지 i를 증가시키며 아래를 수행한다.
- index가 0 이상이고, arr의 stack[index]번째 값이 i번째 값보다 클 때까지 index를 감소시킨다.
- dp의 i번째 위치에 아래를 검증하여 값을 넣어준다.
  - index가 0보다 작으면 처음부터 지금까지 가장 작은 값이므로, $arr[i] \times (i + 1)$ 값을 넣어준다.
  - 위가 아니라면 기존 값에 더해서 추가로 저장해야 하므로, $dp[stack[index]] + arr[i] \times (i - stack[index])$값을 넣어준다.
- result에 dp의 i번째 값을 넣어주고, index를 증가시키고 stack의 index번째 값에 i를 넣어 저장해준다.

4. 반복이 완료되면 result를 모듈러 $10^9 +7$을 적용한 값으로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfSubarrayMinimums.java){:target="_blank"}에서 확인 가능합니다.