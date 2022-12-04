---
title: "Leetcode Java Largest Number At Least Twice of Others"
excerpt: "Leetcode MLargest Number At Least Twice of Others Java"
last_modified_at: 2022-12-04T12:30:00
header:
  image: /assets/images/leetcode/largest-number-at-least-twice-of-others.png
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
[Link](https://leetcode.com/problems/largest-number-at-least-twice-of-others){:target="_blank"}

# 코드
```java
class Solution {

  public int dominantIndex(int[] nums) {
    int max = -1;
    int index = -1;
    int second = -1;
    for (int idx = 0; idx < nums.length; idx++) {
      if (nums[idx] > max) {
        second = max;
        max = nums[idx];
        index = idx;
      } else if (nums[idx] > second) {
        second = nums[idx];
      }
    }
    return max >= second * 2 ? index : -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/854222717/){:target="_blank"}

# 설명
1. nums 내 가장 큰 값이 다른 값보다 최소 두 배 이상 큰지를 검증하여 해당 값의 위치를 반환하는 문제이다.
- 단, 가장 큰 값이 다른 값보다 최소 두 배 이상 크지 않는다면 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 가장 큰 값을 저장할 변수로, -1로 초기화한다.
- index는 가장 큰 값의 위치 값을 저장할 변수로, -1로 초기화한다.
- second는 두 번째로 큰 값을 저장할 변수로, -1로 초기화한다.

3. 0부터 nums의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- nums의 idx번쨰 값이 max보다 큰 경우, 현재까지 가장 큰 값이므로 아래를 수행한다.
  - second에 기존까지 가장 큰 값인 max 값을 넣어준다.
  - max에 현재까지 가장 큰 값인 nums의 idx번째 값을 넣어준다.
  - index에 현재까지 가장 큰 값의 위치인 idx를 넣어준다.
- nums의 idx번쨰 값보다 second의 값이 큰 경우, 두 번째로 큰 값이므로 second에 해당 값을 넣어준다.

4. 반복이 완료되면 max가 second의 두 배 보다 큰 값인지 검증하여 큰 경우 index를, 아니면 -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestNumberAtLeastTwiceOfOthers.java){:target="_blank"}에서 확인 가능합니다.