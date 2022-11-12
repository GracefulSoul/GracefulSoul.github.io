---
title: "Leetcode Java Remove Comments"
excerpt: "Leetcode Remove Comments Java"
last_modified_at: 2022-11-12T12:30:00
header:
  image: /assets/images/leetcode/find-pivot-index.png
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
[Link](https://leetcode.com/problems/find-pivot-index){:target="_blank"}

# 코드
```java
class Solution {

  public int pivotIndex(int[] nums) {
    int sum = 0;
    int half = 0;
    for (int num : nums) {
      sum += num;
    }
    for (int idx = 0; idx < nums.length; idx++) {
      if (half * 2 == sum - nums[idx]) {
        return idx;
      } else {
        half += nums[idx];
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/841712946/){:target="_blank"}

# 설명
1. 피벗 인덱스를 찾는 문제이다.
- 피벗 인덱스란 특정 위치 기준으로 좌측 값들의 합과 우측 값들의 합이 동일한 인덱스이다.
- 피벗 인덱스가 존재하지 않는 경우, -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 nums 내 모든 값들을 더한 값을 저장할 변수로, nums의 모든 값들을 더해준다.
- half는 좌측의 값들을 더해 피벗 인덱스를 구하기 위한 절반 값을 저장할 변수로, 0으로 초기화한다.

3. 0부터 nums의 길이 전까지 idx를 증가시키며 아래를 반복한다.
- half의 2배가 $sum - nums[idx]$를 만족하는 경우, 현재 위치가 피벗 인덱스이므로 idx를 주어진 문제의 결과로 반환한다.
- 위를 만족하지 않는 경우, half에 nums의 idx번째 값을 더해준다.

4. 반복이 완료되면 피벗 인덱스가 존재하지 않으므로 -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindPivotIndex.java){:target="_blank"}에서 확인 가능합니다.