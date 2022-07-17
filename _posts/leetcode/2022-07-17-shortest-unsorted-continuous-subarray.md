---
title: "Leetcode Java Shortest Unsorted Continuous Subarray"
excerpt: "Leetcode Shortest Unsorted Continuous Subarray Java"
last_modified_at: 2022-07-17T22:00:00
header:
  image: /assets/images/leetcode/shortest-unsorted-continuous-subarray.png
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
[Link](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/){:target="_blank"}

# 코드
```java
class Solution {

  public int findUnsortedSubarray(int[] nums) {
    int length = nums.length;
    int start = 0;
    int end = -1;
    int min = nums[length - 1];
    int max = nums[0];
    for (int idx = 1; idx < length; idx++) {
      max = Math.max(max, nums[idx]);
      min = Math.min(min, nums[length - 1 - idx]);
      if (nums[idx] < max) {
        end = idx;
      }
      if (nums[length - 1 - idx] > min) {
        start = length - 1 - idx;
      }
    }
    return end - start + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/749409166/){:target="_blank"}

# 설명
1. nums 내 오름차순 정렬이 필요한 부분 배열의 최소 크기를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- start와 end는 부분 배열의 시작 위치와 종료 위치를 저장한 변수로, 0과 -1로 초기화한다.
- min과 max는 전후의 요소에 대한 크기 검증을 하기위한 변수로, nums의 마지막의 이전 값과 첫 값으로 초기화한다.

3. 1부터 length 미만까지 idx를 증가시키며 아래를 반복한다.
- max에는 max와 nums의 idx번째 값 중 큰 값을 넣어준다.
- min에는 min과 역순으로 탐색하여 nums의 $length - 1 - idx$번째 값 중 작은 값을 넣어준다.
- max가 nums의 idx번째 값보다 큰 경우 이전 값이 더 작으므로, end에 idx를 넣어준다.
- min이 nums의 $length - 1 - idx$번째 값보다 작은 경우 이전 값이 더 크므로, start에 $length - 1 - idx$를 넣어준다.

4. 반복이 완료되면 부분 배열의 크기인 $end - start + 1$을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestUnsortedContinuousSubarray.java){:target="_blank"}에서 확인 가능합니다.