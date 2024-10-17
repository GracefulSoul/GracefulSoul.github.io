---
title: "Leetcode Java Minimum Operations to Reduce X to Zero"
excerpt: "Leetcode Medium - 'Minimum Operations to Reduce X to Zero' 문제 Java 풀이"
last_modified_at: 2023-09-20T22:40:00
header:
  image: /assets/images/leetcode/minimum-operations-to-reduce-x-to-zero.png
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
[Link](https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero){:target="_blank"}

# 코드
```java
class Solution {

  public int minOperations(int[] nums, int x) {
    int sum = 0;
    for (int num : nums) {
      sum += num;
    }
    int max = -1;
    int curr = 0;
    for (int left = 0, right = 0; right < nums.length; right++) {
      curr += nums[right];
      while (left <= right && curr > sum - x) {
        curr -= nums[left++];
      }
      if (curr == sum - x) {
        max = Math.max(max, right - left + 1);
      }
    }
    return max == -1 ? -1 : nums.length - max;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/submissions/1054481507/){:target="_blank"}

# 설명
1. nums의 좌측과 우측의 값을 하나씩 더해서 x가 되는 최소 횟수를 구하는 문제이다.
- 단, 값이 없는 경우 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 nums의 모든 값의 합을 저장할 변수로, nums의 모든 값을 더한 값을 넣어준다.
- max는 남은 값의 최대 갯수를 저장할 변수로, -1로 초기화한다.
- curr은 현재까지 합을 저장할 변수로, 0으로 초기화한다.

3. left와 right는 제거한 숫자의 좌측과 우측의 위치를 저장할 변수로, 둘 다 0으로 초기화하고 right가 nums의 길이 미만까지 증가시키며 아래를 반복한다.
- curr에 nums[right]의 값을 더해준다.
- left가 right보다 같거나 작고, curr이 $sum - x$보다 클 때 까지 curr에 nums[left]의 값을 빼고 left를 증가시킨다.
- curr이 $sum - x$와 동일한 경우, max에 max와 $right - left + 1$인 잔여 값의 갯수 중 큰 값을 저장한다.

4. 반복이 완료되면 max가 -1인지 검증하여 -1이면 -1을, 아니면 nums의 길이에서 max를 뺀 최소 횟수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumOperationsToReduceXToZero.java){:target="_blank"}에서 확인 가능합니다.