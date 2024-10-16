---
title: "Leetcode Java Binary Subarrays With Sum"
excerpt: "Leetcode Binary Subarrays With Sum Java"
last_modified_at: 2023-06-11T08:00:00
header:
  image: /assets/images/leetcode/binary-subarrays-with-sum.png
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
[Link](https://leetcode.com/problems/binary-subarrays-with-sum){:target="_blank"}

# 코드
```java
class Solution {

  public int numSubarraysWithSum(int[] nums, int goal) {
    int sum = 0;
    int result = 0;
    int[] count = new int[nums.length + 1];
    count[0] = 1;
    for (int num : nums) {
      sum += num;
      if (sum >= goal) {
        result += count[sum - goal];
      }
      count[sum]++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/binary-subarrays-with-sum/submissions/968396163/){:target="_blank"}

# 설명
1. 0과 1로 이루어진 nums의 연속된 값들의 합이 goal이 되는 부분 배열의 수를 구하는 문제다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 합을 계산하기 위한 임시 변수로, 0으로 초기화한다.
- result는 하위 부분 배열의 수를 구하기 위한 변수로, 0으로 초기화한다.
- count는 연속된 값의 합계인 위치의 갯수를 계산할 변수로, nums의 길이보다 1 큰 크기로 초기화하여 첫 값에 1로 초기화한다.

3. nums의 모든 값을 num에 넣어 순차적으로 반복한다.
- sum에 num을 더해준다.
- sum이 goal보다 큰 경우, result에 count의 $sum - goal$ 위치의 값을 더해준다.
- count의 sum번째 값을 증가시킨다.

4. nums의 연속된 값들의 합이 goal이 되는 부분 배열의 수를 계산한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinarySubarraysWithSum.java){:target="_blank"}에서 확인 가능합니다.