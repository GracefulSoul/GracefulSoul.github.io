---
title: "Leetcode Java Length of Longest Subarray With at Most K Frequency"
excerpt: "Leetcode Length of Longest Subarray With at Most K Frequency Java"
last_modified_at: 2024-03-29T18:50:00
header:
  image: /assets/images/leetcode/count-subarrays-where-max-element-appears-at-least-k-times.png
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
[Link](https://leetcode.com/problems/count-subarrays-where-max-element-appears-at-least-k-times/){:target="_blank"}

# 코드
```java
class Solution {

  public long countSubarrays(int[] nums, int k) {
    int max = 0;
    for (int num : nums) {
      max = Math.max(max, num);
    }
    long result = 0;
    for (int i = 0, j = 0; j < nums.length; j++) {
      k -= nums[j] == max ? 1 : 0;
      while (k == 0) {
        k += nums[i++] == max ? 1 : 0;
      }
      result += i;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-subarrays-where-max-element-appears-at-least-k-times/submissions/1217183878/){:target="_blank"}

# 설명
1. nums내 동일한 값이 정확히 k번 나타나는 부분 배열의 수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 nums 내 가장 큰 값을 저장할 변수로, nums를 반복하여 가장 큰 값을 찾아 넣어준다.
- result는 부분 배열의 수를 저장할 변수로, 0으로 초기화한다.

3. i는 0으로, j는 0부터 nums의 길이 미만까지 증가시키며 아래를 수행한다.
- k에 nums[j]의 값이 max와 동일하면 1을 빼준다.
- k가 0이 될 때까지 k에 nums[i]의 값이 max와 동일하면 조건에 부합하므로 1을 더해주고 i를 증가시킨다.
- result에 부분 배열의 수인 i를 더해준다.

4. 반복이 완료되면 부분 배열의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountSubarraysWhereMaxElementAppearsAtLeastKTimes.java){:target="_blank"}에서 확인 가능합니다.