---
title: "Leetcode Java Count Subarrays With Fixed Bounds"
excerpt: "Leetcode Hard - 'Count Subarrays With Fixed Bounds' 문제 Java 풀이"
last_modified_at: 2024-03-31T17:30:00
header:
  image: /assets/images/leetcode/count-subarrays-with-fixed-bounds.png
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
[Link](https://leetcode.com/problems/count-subarrays-with-fixed-bounds/){:target="_blank"}

# 코드
```java
class Solution {

  public long countSubarrays(int[] nums, int minK, int maxK) {
    long result = 0;
    int bad = -1;
    int min = -1;
    int max = -1;
    for (int i = 0; i < nums.length; i++) {
      if (nums[i] < minK || nums[i] > maxK) {
        bad = i;
      }
      if (nums[i] == minK) {
        min = i;
      }
      if (nums[i] == maxK) {
        max = i;
      }
      result += Math.max(0L, Math.min(min, max) - bad);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-subarrays-with-fixed-bounds/submissions/1219022736/){:target="_blank"}

# 설명
1. nums 내 [minK, maxK] 범위 내인 값들만 존재하는 부분 배열의 수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 부분 배열의 수를 저장할 변수로, 0으로 초기화한다.
- bad는 범위를 벗어나는 값의 마지막 위치를 저장할 변수로, -1로 초기화한다.
- min과 max는 최소 최대가 되는 위치를 저장할 변수로, -1로 초기화한다.

3. 0부터 nums의 길이 미만일 때 까지 i를 증가시키며 아래를 반복한다.
- nums[i]의 값이 [minK, maxK] 범위를 벗어나면, bad에 현재 위치인 i를 넣어준다.
- nums[i]의 값이 minK의 값과 동일하면 min에 i를, maxK의 값과 동일하면 max에 i를 넣어준다.
- result에 min과 max중 작은 값에 bad를 뺀 조건에 맞는 부분 배열의 수를 음수인 경우를 제외하고 더해준다.

4. 반복이 완료되면 부분 배열의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountSubarraysWithFixedBounds.java){:target="_blank"}에서 확인 가능합니다.