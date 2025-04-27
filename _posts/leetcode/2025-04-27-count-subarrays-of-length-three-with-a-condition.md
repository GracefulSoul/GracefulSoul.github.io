---
title: "Leetcode Java Count Subarrays of Length Three With a Condition"
excerpt: "Leetcode - 'Count Subarrays of Length Three With a Condition' 문제 Java 풀이"
last_modified_at: 2025-04-27T16:40:00
header:
  image: /assets/images/leetcode/count-subarrays-of-length-three-with-a-condition.png
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
[Link](https://leetcode.com/problems/count-subarrays-of-length-three-with-a-condition/){:target="_blank"}

# 코드
```java
class Solution {

  public int countSubarrays(int[] nums) {
    int result = 0;
    for (int i = 0; i < nums.length - 2; i++) {
      if (2 * (nums[i] + nums[i + 2]) == nums[i + 1]) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-subarrays-of-length-three-with-a-condition/submissions/1619121097/){:target="_blank"}

# 설명
1. nums 내 연속된 세 숫자의 가운데 값이 나머지 두 값의 두 배가 되는 부분 배열의 갯수를 계산하는 문제이다.

2. nums의 연속된 세 숫자를 반복하여 $2 \times (nums[i] + nums[i + 2]) = nums[i + 1]$이 성립하는 부분 배열의 갯수를 계산하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountSubarraysOfLengthThreeWithACondition.java){:target="_blank"}에서 확인 가능합니다.