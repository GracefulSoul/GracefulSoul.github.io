---
title: "Leetcode Java Find the Maximum Sum of Node Values"
excerpt: "Leetcode Find the Maximum Sum of Node Values Java"
last_modified_at: 2024-05-19T12:10:00
header:
  image: /assets/images/leetcode/find-the-maximum-sum-of-node-values.png
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
[Link](https://leetcode.com/problems/find-the-maximum-sum-of-node-values/){:target="_blank"}

# 코드
```java
class Solution {

  public long maximumValueSum(int[] nums, int k, int[][] edges) {
    long result = 0;
    int count = 0;
    int min = Integer.MAX_VALUE;
    int max = Integer.MIN_VALUE;
    for (int num : nums) {
      result += num;
      int value = (num ^ k) - num;
      if (value > 0) {
        min = Math.min(min, value);
        result += value;
        count++;
      } else {
        max = Math.max(max, value);
      }
    }
    if (count % 2 == 0) {
      return result;
    } else {
      return Math.max(result - min, result + max);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-maximum-sum-of-node-values/submissions/1261791228/){:target="_blank"}

# 설명
1. 각 점수가 담긴 nums를 이용하여 0번 혹은 모든 edges 내 각 지점에 k를 XOR 비트 연산을 수행한 nums의 합이 최대가 되는 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장할 변수로, 0으로 초기화한다.
- count는 nums의 각 값에 k를 XOR 비트 연산을 수행한 값이 기존 값보다 큰 갯수를 저장할 변수로, 0으로 초기화한다.
- min과 max는 nums의 각 값에 k를 XOR 비트 연산을 수행한 값을 기존값과 뺀 결과의 경우에 따른 최솟값 최댓값을 저장할 변수로, 정수의 최댓값과 최솟값으로 초기화한다.

3. nums의 각 값을 num에 순차적으로 넣어 아래를 수행한다.
- result에 num을 더해준다.
- value에 num에 k를 XOR 비트 연산을 수행한 값에 num을 빼준다.
- value가 0 초과인 경우, 아래를 수행한다.
  - min에 min과 value 중 작은 값을 넣어준다.
  - result에 value를 더해 결과 값을 증가시켜준 후, 기존 값보다 큰 갯수를 저장한 count를 증가시킨다.
- value가 0 이하인 경우, max에 max와 value 중 큰 값을 저장한다.

4. 반복이 완료되면 count가 짝수인지 홀수인지 검증하여 결과를 반환한다.
- count가 짝수인 경우 result가 항상 최대가 되므로, result를 주어진 문제의 결과로 반환한다.
- count가 홀수인 경우 최솟값을 빼거나 최댓값을 더한 경우가 최대가 되므로, $result - min$과 $result + max$ 중 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheMaximumSumOfNodeValues.java){:target="_blank"}에서 확인 가능합니다.