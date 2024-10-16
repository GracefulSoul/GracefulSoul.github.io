---
title: "Leetcode Java Sum of Subsequence Widths"
excerpt: "Leetcode Sum of Subsequence Widths Java"
last_modified_at: 2023-04-02T14:40:00
header:
  image: /assets/images/leetcode/sum-of-subsequence-widths.png
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
[Link](https://leetcode.com/problems/sum-of-subsequence-widths){:target="_blank"}

# 코드
```java
class Solution {

  public int sumSubseqWidths(int[] nums) {
    Arrays.sort(nums);
    long c = 1;
    long result = 0;
    long mod = 1000000007L;
    for (int i = 0, j = nums.length - 1; i < nums.length; i++, j--) {
      result = (result + (nums[i] * c) - (nums[j] * c)) % mod;
      c = (c * 2) % mod;
    }
    return (int) ((result + mod) % mod);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sum-of-subsequence-widths/submissions/926405251/){:target="_blank"}

# 설명
1. nums 배열 내 값들의 부분 배열의 모든 너비의 합을 계산하는 문제이다.
- 너비는 최대 요소와 최소 요소의 차이 값을 의미한다.
- 값이 매우 클 수 있으므로 모듈러 $10^9 +7$로 결과를 반환한다.

2. nums를 오름차순으로 정렬해준다.

3. 문제 해결에 필요한 변수를 정의한다.
- c는 2배수를 저장할 변수로, 1로 초기화한다.
- result는 너비의 합을 저장할 변수로 0으로 초기화한다.
- mod는 모듈러를 적용할 변수로, $10^9 +7$로 초기화한다.

4. 0부터 nums의 길이 미만까지 i를 증가시키고, j는 nums의 길이보다 1 작은 값부터 j를 감소시키며 아래를 반복한다.
- result에 result와 $nums[i] \times c$와 $nums[j] \times c$의 차이를 더해서 mod로 나눈 나머지 값을 넣어준다.
- c에 $c \times 2$에 mod로 나눈 값을 넣어준다.

5. 반복이 완료되면 result와 mod의 합을 mod로 나눈 나머지 값을 주어진 문제의 결과로 반환한다.

# 풀이
- nums의 i번째 위치에서 좌측으로 $2^i$개의 부분 배열이 존재하므로, result에 $nums[i] \times 2^i$를 더해준다.
- nums의 i번째 위치에서 우측으로 $2^j$개의 부분 배열이 존재하므로, result에 $nums[j] \times 2&j$의 값을 빼준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfSubsequenceWidths.java){:target="_blank"}에서 확인 가능합니다.