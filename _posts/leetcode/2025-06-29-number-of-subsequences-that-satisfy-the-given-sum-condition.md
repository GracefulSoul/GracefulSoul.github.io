---
title: "Leetcode Java Number of Subsequences That Satisfy the Given Sum Condition"
excerpt: "Leetcode - 'Number of Subsequences That Satisfy the Given Sum Condition' 문제 Java 풀이"
last_modified_at: 2025-06-29T09:45:00
header:
  image: /assets/images/leetcode/number-of-subsequences-that-satisfy-the-given-sum-condition.png
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
[Link](https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/){:target="_blank"}

# 코드
```java
class Solution {

  private static final int MOD = 1000000007;

  public int numSubseq(int[] nums, int target) {
    Arrays.sort(nums);
    int result = 0;
    int length = nums.length;
    int[] pows = new int[length];
    pows[0] = 1;
    for (int i = 1; i < length; i++) {
      pows[i] = (2 * pows[i - 1]) % MOD;
    }
    int left = 0;
    int right = length - 1;
    while (left <= right) {
      if (nums[left] + nums[right] > target) {
        right--;
      } else {
        result = (result + pows[right - left++]) % MOD;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/submissions/1679787095/){:target="_blank"}

# 설명
1. 정수 배열 nums를 이용하여 부분 수열의 값이 최댓값과 최솟값의 차잇값이 target 이하인 부분 수열의 갯수를 계산하는 문제이다.
- 단, 값이 매우 클 수 있으므로, 모듈러 $10^9 + 7$을 적용한다.

2. 문제 풀이에 필요한 변수를 정의 및 정렬한다.
- nums를 오름차순으로 정렬한다.
- result는 부분 수열의 갯수를 계산할 변수로, 0으로 초기화한다.
- length는 nums의 길이를 저장한 변수이다.
- pows는 2의 거듭제곱값을 저장할 변수로, length 길이의 정수 배열로 초기화하고 첫 값을 1로 넣어주고 각 위치에 해당 위치에 해당하는 2의 거듭제곱 값을 모듈러를 적용한 값으로 넣어준다.
- left와 right는 nums의 위치 변수로, 0과 $length - 1$로 초기화한다.

3. left가 right 이하까지 아래를 반복한다.
- $nums[left] + nums[right]$의 값이 target보다 큰 경우, right를 감소시켜 범위를 좁혀준다.
- 위의 경우가 아니라면 조건에 만족하므로, result에 $result + pows[right - left]$ 값에 모듈러를 적용한 값으로 넣어준다.

4. 반복이 완료되면 계산된 부분 수열의 갯수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindSubsequenceOfLengthKWithTheLargestSum.java){:target="_blank"}에서 확인 가능합니다.