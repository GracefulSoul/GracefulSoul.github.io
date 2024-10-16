---
title: "Leetcode Java Longest Consecutive Sequence"
excerpt: "Leetcode Longest Consecutive Sequence Java 풀이"
last_modified_at: 2021-08-17T14:40:00
header:
  image: /assets/images/leetcode/longest-consecutive-sequence.png
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
[Link](https://leetcode.com/problems/longest-consecutive-sequence/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestConsecutive(int[] nums) {
    if (nums.length == 0) {
      return 0;
    }
    Arrays.sort(nums);
    int curr = nums[0];
    int sum = 1;
    int count = 1;
    for (int i = 1; i < nums.length; i++) {
      if (nums[i - 1] == nums[i]) {
        continue;
      } else if (nums[i] == curr + 1) {
        curr++;
        sum++;
        count = Math.max(count, sum);
      } else {
        curr = nums[i];
        sum = 1;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/539682680/){:target="_blank"}

# 설명
1. 주어진 숫자 배열 nums의 값들을 이용하여 가장 많이 연속된 숫자의 개수를 계산하는 문제이다.

2. 배열 nums가 비어있을 경우, 주어진 문제의 결과로 0을 반환한다.

3. 연속된 숫자들을 효율적으로 확인하기 위해서 배열을 정렬해준다.

4. 문제 풀이에 필요한 변수를 정의한다.
- curr은 주어진 배열 nums의 값을 하나씩 가져와 저장할 임시 변수로, nums[0]으로 초기화 한다.
- sum은 연속된 숫자의 합을 저장할 변수로, 1로 초기화 한다.
- count는 연속된 숫자의 개수가 최대인 값을 저장하는 변수로, 1로 초기화 한다.

5. 주어진 배열 nums를 반복하여 연속된 숫자가 최대인 개수를 계산한다.
- nums[$i - 1$]의 값과 nums[i]의 값이 동일하면, 반복 계속 진행한다.
- nums[i]의 값이 $curr + 1$이면 curr과 sum을 증가시키고, sum과 count 중 큰 값을 count에 넣어준다.
- 그 외의 경우 연속된 숫자가 아니므로, curr에 nums[i]를 넣고 sum을 1로 초기화 한다.

6. 반복이 완료되면 연속된 숫자의 개수가 최대인 값을 저장한 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestConsecutiveSequence.java){:target="_blank"}에서 확인 가능합니다.