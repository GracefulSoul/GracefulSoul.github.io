---
title: "Leetcode Java House Robber IV"
excerpt: "Leetcode - 'House Robber IV' 문제 Java 풀이"
last_modified_at: 2025-03-15T13:00:00
header:
  image: /assets/images/leetcode/house-robber-iv.png
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
[Link](https://leetcode.com/problems/house-robber-iv/){:target="_blank"}

# 코드
```java
class Solution {

  public int minCapability(int[] nums, int k) {
    int left = Integer.MAX_VALUE;
    int right = 0;
    for (int num : nums) {
      left = Math.min(left, num);
      right = Math.max(right, num);
    }
    int length = nums.length;
    while (left < right) {
      int mid = left + (right - left) / 2;
      int count = 0;
      int i = 0;
      while (i < length) {
        if (nums[i++] <= mid) {
          count++;
          i++;
        }
      }
      if (count >= k) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }
    return left;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/house-robber-iv/submissions/1574079010/){:target="_blank"}

# 설명
1. nums는 각 집에 보유한 달러를 저장한 배열로 인접하지 않은 k개 집을 털 때, 최대 털수 있는 달러의 경우 중 가장 최소로 털 수 있는 달러를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- left와 right는 탐색에 필요한 위치 변수로, nums의 최솟값과 최댓값을 넣어준다.
- length는 nums의 길이를 저장한 변수이다.

3. left가 right 미만일 때 까지 아래를 반복한다.
- mid에 $left + \frac{right - left}{2}$인 중앙값을 넣어준다.
- count는 턴 집의 갯수를 저장할 변수로, 0으로 초기화한다.
- i는 nums의 위치 변수로, 0으로 초기화한다.
- i가 length 미만까지 아래를 반복한다.
  - nums[i]의 값이 mid 이하인 경우, count와 i를 증가시키고 i를 다시 증가시켜준다.
  - count가 k 이상인 조건에 충저한 경우, right에 mid를 넣고 그렇지 않으면 left에 $mid + 1$을 넣어 범위를 좁혀준다.

4. 반복이 완료되면 최소 달러인 left를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/HouseRobberIV.java){:target="_blank"}에서 확인 가능합니다.