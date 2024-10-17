---
title: "Leetcode Java Maximum Sum of Two Non-Overlapping Subarrays"
excerpt: "Leetcode Medium - 'Maximum Sum of Two Non-Overlapping Subarrays' 문제 Java 풀이"
last_modified_at: 2024-01-29T19:20:00
header:
  image: /assets/images/leetcode/maximum-sum-of-two-non-overlapping-subarrays.png
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
[Link](https://leetcode.com/problems/maximum-sum-of-two-non-overlapping-subarrays){:target="_blank"}

# 코드
```java
class Solution {

  public int maxSumTwoNoOverlap(int[] nums, int firstLen, int secondLen) {
    return Math.max(this.maxSum(nums, firstLen, secondLen), this.maxSum(nums, secondLen, firstLen));
  }

  private int maxSum(int[] nums, int firstLen, int secondLen) {
    int sumFirstLen = 0;
    int sumSecondLen = 0;
    for (int i = 0; i < firstLen + secondLen; i++) {
      if (i < firstLen) {
        sumFirstLen += nums[i];
      } else {
        sumSecondLen += nums[i];
      }
    }
    int result = sumFirstLen  + sumSecondLen;
    for (int i = firstLen + secondLen, max = sumFirstLen; i < nums.length; i++) {
      sumFirstLen += nums[i - secondLen] - nums[i - firstLen - secondLen];
      sumSecondLen += nums[i] - nums[i - secondLen];
      max = Math.max(max, sumFirstLen);
      result = Math.max(result, max + sumSecondLen);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-sum-of-two-non-overlapping-subarrays/submissions/1159974265/){:target="_blank"}

# 설명
1. nums의 firstLen 크기와 secondLen 크기의 겹치지 않은 연속된 부분 배열들의 합이 최대인 값을 구하는 문제이다.

2. 3번에서 정의한 maxSum(int[] nums, int firstLen, int secondLen)에 firstLen과 secondLen을 순서를 바꾸어 각각 수행한 결과 중 큰 값을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- sumFirstLen과 sumSecondLen은 firstLen과 secondLen 크기의 연속된 부분 배열의 값의 합을 저장할 변수로, nums의 firstLen개의 값과 그 다음 secondLen개의 값을 각각 더해준다.
- result는 부분 배열들의 합을 저장할 변수로, sumSecondLen과 sumFirstLen의 값을 더해서 넣어준다.
- $firstLen + secondLen$부터 nums의 길이 미만까지 i를 증가시키고, max에 sumFirstLen을 넣어 아래를 반복한다.
  - sumFirstLen에 다음 위치 값인 nums[$i - secondLen$] 값을 더한 후, 제거 할 좌측 값인 nums[$i - firstLen - secondLen$] 값을 빼준다.
  - sumSecondLen에 다음 위치 값인 nums[i] 값을 더한 후, 제거 할 좌측 값인 nums[$i - secondLen$] 값을 빼준다.
  - max에 이전까지 첫 부분 배열의 최댓값인 max와 현재 첫 부분 배열의 합인 sumFirstLen 중 큰 값을 넣어준다.
  - result에 이전까지 최댓값인 result와 현재 값들의 합인 $max + sumSecondLen$ 중 큰 값을 넣어준다.

4. 반복이 완료되면 각 구간의 합이 최대가 되는 결과가 저장된 result를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumSumOfTwoNonOverlappingSubarrays.java){:target="_blank"}에서 확인 가능합니다.