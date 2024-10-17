---
title: "Leetcode Java Longest Harmonious Subsequence"
excerpt: "Leetcode - 'Longest Harmonious Subsequence' 문제 Java 풀이"
last_modified_at: 2022-07-25T19:00:00
header:
  image: /assets/images/leetcode/longest-harmonious-subsequence.png
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
[Link](https://leetcode.com/problems/longest-harmonious-subsequence/){:target="_blank"}

# 코드
```java
class Solution {

  public int findLHS(int[] nums) {
    Arrays.sort(nums);
    int max = 0;
    for (int idx = 0; idx < nums.length; idx++) {
      if (idx == 0 || nums[idx] != nums[idx - 1]) {
        int next = idx + 1;
        int curr = nums[idx];
        int length = 1;
        while (next < nums.length && nums[next] - curr <= 1) {
          length++;
          next++;
        }
        if (nums[next - 1] - curr == 1 && length > max) {
          max = length;
        }
      }
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/756191194/){:target="_blank"}

# 설명
1. nums의 최댓값과 최솟값의 차이가 1인 가장 긴 부분 배열의 길이를 구하는 문제이다.

2. nums를 오름차순으로 정렬한다.

3. max는 부분 배열의 최대 길이를 담을 변수로, 0으로 초기화한다

4. 0부터 nums의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- idx가 0이거나 nums의 idx번째 값과 $idx - 1$번째 값이 동일하지 않은 경우 아래를 수행한다.
  - next에 $idx + 1$을, curr에 nums의 idx번째 값을, length를 1을 넣어 초기화한다.
  - next가 nums의 길이보다 작고 nums의 next번째 값과 curr의 차이가 1 이하인 경우, length와 next를 증가시킨다.
  - nums의 $next - 1$번째 값과 curr의 차이가 1이고 length가 max보다 큰 경우, max에 length를 넣어준다.

5. 반복이 완료되면 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestHarmoniousSubsequence.java){:target="_blank"}에서 확인 가능합니다.