---
title: "Leetcode Java Count Subarrays With Score Less Than K"
excerpt: "Leetcode - 'Count Subarrays With Score Less Than K' 문제 Java 풀이"
last_modified_at: 2025-04-28T19:40:00
header:
  image: /assets/images/leetcode/count-subarrays-with-score-less-than-k.png
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
[Link](https://leetcode.com/problems/count-subarrays-with-score-less-than-k/){:target="_blank"}

# 코드
```java
class Solution {

  public long countSubarrays(int[] nums, long k) {
    long sum = 0;
    long result = 0;
    for (int i = 0, j = 0; j < nums.length; j++) {
      sum += nums[j];
      while (sum * (j - i + 1) >= k) {
        sum -= nums[i++];
      }
      result += j - i + 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-subarrays-of-length-three-with-a-condition/submissions/1619121097/){:target="_blank"}

# 설명
1. nums 내 아래 규칙을 만족하는 k 점수 미만의 부분 배열 갯수를 반환하는 문제이다.
- 부분 배열 [1, 2, 3, 4, 5]의 값은 $(1 + 2 + 3 + 4 + 5) \times 5$ 점수를 획득한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 합계를 저장할 변수로, 0으로 초기화한다.
- result는 k 점수 이하의 부분 배열 갯수를 계산할 변수로, 0으로 초기화한다.

3. i는 0으로, j는 0부터 nums의 길이 미만까지 증가시키며 아래를 반복한다.
- sum에 nums[j]의 값을 더해준다.
- $sum \times (j - i + 1)$의 값이 k 이상인 조건에 부합하는 값일 때 까지, sum에 nums[i]의 값을 빼주고 i를 증가시켜준다.
- result에 $j - i + 1$인 가능한 부분 배열의 갯수를 더해준다.

4. 반복이 완료되면 k 점수 미만의 부분 배열의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountSubarraysWithScoreLessThanK.java){:target="_blank"}에서 확인 가능합니다.