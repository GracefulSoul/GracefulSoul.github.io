---
title: "Leetcode Java Length of Longest Subarray With at Most K Frequency"
excerpt: "Leetcode Length of Longest Subarray With at Most K Frequency Java"
last_modified_at: 2024-03-28T18:50:00
header:
  image: /assets/images/leetcode/length-of-longest-subarray-with-at-most-k-frequency.png
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
[Link](https://leetcode.com/problems/length-of-longest-subarray-with-at-most-k-frequency/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxSubarrayLength(int[] nums, int k) {
    Map<Integer, Integer> count = new HashMap<>();
    int result = 0;
    for (int i = 0, j = 0; j < nums.length; j++) {
      count.put(nums[j], count.getOrDefault(nums[j], 0) + 1);
      while (count.get(nums[j]) > k) {
        count.put(nums[i], count.get(nums[i++]) - 1);
      }
      result = Math.max(result, j - i + 1);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/length-of-longest-subarray-with-at-most-k-frequency/submissions/1216247472/){:target="_blank"}

# 설명
1. nums 내 숫자의 갯수가 k개 이하인 부분 배열 중 가장 긴 부분 배열의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 nums 내 숫자의 갯수를 계산할 변수로, HashMap으로 초기화한다.
- result는 가장 긴 부분 배열의 길이를 저장할 변수로, 0으로 초기화한다.

3. i는 0으로, j는 0부터 nums의 길이 미만까지 j를 증가시키며 아래를 반복한다.
- count에 nums[j]에 해당하는 갯수를 증가시켜준다.
- count의 nums[j]에 해당하는 갯수가 k 초과일 때 까지 count의 nums[i]에 해당하는 갯수를 감소시키고 i를 증가시킨다.
- result에 result와 $j - i + 1$인 현재까지의 부분 배열의 길이 중 큰 값을 넣어준다.

4. 반복이 완료되면 가장 긴 부분 배열의 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LengthOfLongestSubarrayWithAtMostKFrequency.java){:target="_blank"}에서 확인 가능합니다.