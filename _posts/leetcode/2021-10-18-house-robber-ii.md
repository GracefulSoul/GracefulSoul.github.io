---
title: "Leetcode Java House Robber II"
excerpt: "Leetcode - 'House Robber II' 문제 Java 풀이"
last_modified_at: 2021-10-18T13:00:00
header:
  image: /assets/images/leetcode/house-robber-ii.png
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
[Link](https://leetcode.com/problems/house-robber-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int rob(int[] nums) {
    if (nums.length == 1) {
      return nums[0];
    } else {
      return Math.max(this.getMax(nums, 0), this.getMax(nums, 1));
    }
  }

  private int getMax(int[] nums, int start) {
    int pre = 0;
    int cur = 0;
    for (int i = start; i < nums.length + start - 1; i++) {
      int temp = cur;
      cur = Math.max(pre + nums[i], cur);
      pre = temp;
    }
    return cur;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/573012065/){:target="_blank"}

# 설명
1. 지난번 [House Robber](../house-robber){:target="_blank"}와 유사한 문제로, 주어진 정수 배열 nums를 이용하여 인접하지 않은 값들의 합이 가장 큰 값을 찾는 문제이다.
- 단, 주어진 배열 nums의 처음 값과 마지막 값은 인접하다고 판단한다.

2. 주어진 배열 nums의 길이가 1이면 값이 하나밖에 없으므로 최댓값인 nums[0]을 주어진 문제의 결과로 반환한다.

3. 그 외의 경우 첫 값을 제외한 경우와, 마지막 값을 제외한 경우 중 가장 큰 값을 주어진 문제의 결과로 반환한다.
- 문제의 조건 중 처음 값과 마지막 값이 인접하다는 조건이 있으므로, 첫 값을 제외한 경우와 마지막 값을 제외한 경우의 두 경우를 확인하는 것이다.
- 이전까지 최댓값을 저장할 변수인 pre와 현재의 최댓값을 저장할 변수인 cur을 정의한다.
- start부터 $nums.length + start - 1$까지 반복하여 아래를 수행한다.
  - 지역 변수인 temp를 정의하여 cur의 값을 임시 저장시킨다.
  - cur에 $pre + nums[i]$와 cur의 값 중 큰 값을 넣어 인접하지 않은 값들의 최댓값을 저장시킨다.
  - pre에 그 전까지 최댓값이었던 temp 값을 넣어주고 반복을 계속 수행한다.
- 반복이 완료되면 최댓값을 저장한 cur을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HouseRobberII.java){:target="_blank"}에서 확인 가능합니다.