---
title: "Leetcode Java Longest Nice Subarray"
excerpt: "Leetcode - 'Longest Nice Subarray' 문제 Java 풀이"
last_modified_at: 2025-03-18T21:20:00
header:
  image: /assets/images/leetcode/longest-nice-subarray.png
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
[Link](https://leetcode.com/problems/longest-nice-subarray/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestNiceSubarray(int[] nums) {
    int result = 0;
    int i = 0;
    int and = 0;
    for (int j = 0; j < nums.length; j++) {
      while ((and & nums[j]) > 0) {
        and ^= nums[i++];
      }
      and |= nums[j];
      result = Math.max(result, j - i + 1);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/divide-array-into-equal-pairs/submissions/1576563375/){:target="_blank"}

# 설명
1. nums 내 인근 값의 AND 비트 연산의 결과가 0이 되는 최대 부분 배열의 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최대 부분 배열의 길이를 저장할 변수로, 0으로 초기화한다.
- i는 부분 배열의 시작 위치를 저장할 변수로, 0으로 초기화한다.
- and는 인접한 두 값의 and 비트 연산의 결과를 계산할 변수로, 0으로 초기화한다.

3. 0부터 nums의 길이 미만까지 j를 증가시키면서 아래를 반복한다.
- and와 nums[j]의 AND 비트 연산의 결과가 0보다 클 때까지, and에 and와 nums[i]의 값을 XOR 비트 연산의 결과를 넣어주고 i를 증가시킨다.
- and에 nums[j]인 현재 위치 값을 OR 비트 연산을 수행하여 넣어 마지막 값으로 저장한다.
- result에 result와 $j - i + 1$인 현재까지 부분 배열의 길이 중 큰 값을 넣어준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestNiceSubarray.java){:target="_blank"}에서 확인 가능합니다.