---
title: "Leetcode Java Minimum Number of K Consecutive Bit Flips"
excerpt: "Leetcode Minimum Number of K Consecutive Bit Flips Java"
last_modified_at: 2023-09-22T18:50:00
header:
  image: /assets/images/leetcode/minimum-number-of-k-consecutive-bit-flips.png
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
[Link](https://leetcode.com/problems/minimum-number-of-k-consecutive-bit-flips){:target="_blank"}

# 코드
```java
class Solution {

  public int minKBitFlips(int[] nums, int k) {
    int length = nums.length;
    int curr = 0;
    int result = 0;
    for (int i = 0; i < length; i++) {
      if (i >= k && nums[i - k] > 1) {
        curr--;
        nums[i - k] -= 2;
      }
      if (curr % 2 == nums[i]) {
        if (i + k > length) {
          return -1;
        }
        nums[i] += 2;
        curr++;
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-k-consecutive-bit-flips/submissions/1056170903/){:target="_blank"}

# 설명
1. 0과 1로 이루어진 num의 값을 연속된 k개의 값을 뒤집을 때, 0이 없어지기 위한 최소 횟수를 구하는 문제이다.
- 0을 모두 없앨 수 없으면, -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- curr은 현재 위치를 저장할 변수로, 0으로 초기화한다.
- result는 최소 횟수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- i가 k 이상이면서 num의 $i - k$번째 값이 1보다 큰 경우, 뒤집은 이력이 있으므로 curr을 감소시키고 nums의 $i - k$번째 값을 2 감소시킨다.
- curr을 2로 나눈 나머지가 nums[i]와 같은 경우, 아래를 수행한다.
  - $i + k$가 length보다 큰 경우, 0을 모두 없앨 수 없으므로 -1을 주어진 문제의 결과로 반환한다.
- nums[i]에 2를 증가시키고, curr과 result를 증가시켜 다음 위치로 이동하면서 뒤집은 횟수를 증가시킨다.

4. 반복이 완료되면 뒤집은 횟수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumOperationsToReduceXToZero.java){:target="_blank"}에서 확인 가능합니다.