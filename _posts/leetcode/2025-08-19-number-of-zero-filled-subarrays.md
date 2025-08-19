---
title: "Leetcode Java Number of Zero-Filled Subarrays"
excerpt: "Leetcode - 'Number of Zero-Filled Subarrays' 문제 Java 풀이"
last_modified_at: 2025-08-19T18:20:00
header:
  image: /assets/images/leetcode/number-of-zero-filled-subarrays.png
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
[Link](https://leetcode.com/problems/number-of-zero-filled-subarrays/){:target="_blank"}

# 코드
```java
class Solution {

  public long zeroFilledSubarray(int[] nums) {
    long count = 0;
    long result = 0;
    for (int i = 0; i < nums.length; i++) {
      if (nums[i] == 0) {
        result += ++count;
      } else {
        count = 0;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-zero-filled-subarrays/submissions/1740630254/){:target="_blank"}

# 설명
1. nums 내 연속된 0으로 구성된 부분 배열의 갯수를 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 연속된 0으로 구성할 수 있는 부분 배열의 갯수를 계산하기 위한 변수로, 0으로 초기화한다.
- result는 총 부분 배열의 갯수를 계산하기 위한 변수로, 0으로 초기화한다.

3. 0부터 nums의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- nums[i]의 값이 0인 경우, count를 증가시킨 후 result에 값을 더해준다.
- nums[i]의 값이 0이 아닌 경우, count를 0으로 초기화시켜준다.

4. 반복이 완료되면 총 부분 배열의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfZeroFilledSubarrays.java){:target="_blank"}에서 확인 가능합니다.