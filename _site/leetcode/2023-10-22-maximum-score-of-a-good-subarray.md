---
title: "Leetcode Java Maximum Score of a Good Subarray"
excerpt: "Leetcode Maximum Score of a Good Subarray Java"
last_modified_at: 2023-10-22T13:30:00
header:
  image: /assets/images/leetcode/maximum-score-of-a-good-subarray.png
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
[Link](https://leetcode.com/problems/maximum-score-of-a-good-subarray){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumScore(int[] nums, int k) {
    int length = nums.length;
    int i = k - 1;
    int j = k + 1;
    int min = nums[k];
    while (0 <= i && min <= nums[i]) {
      i--;
    }
    while (j < length && min <= nums[j]) {
      j++;
    }
    int result = min * (j - i - 1);
    while (0 <= i || j < length) {
      if (i < 0 || (j < length && nums[i] <= nums[j])) {
        min = nums[j];
        while (j < length && min <= nums[j]) {
          j++;
        }
      } else {
        min = nums[i];
        while (0 <= i && min <= nums[i]) {
          i--;
        }
      }
      result = Math.max(result, min * (j - i - 1));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-score-of-a-good-subarray/submissions/1081083175/){:target="_blank"}

# 설명
1. nums의 좋은 부분 배열의 최대 점수를 구하는 문제이다.
- 좋은 부분 배열은 i <= k <= j 를 만족하는 i ~ j 번째 값들의 배열이다.
- 점수는 i ~ j 번째 값들 내 최솟값과 $j - i + 1$을 곱한 값으로 계산한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- min은 nums 내 최솟값을 저장할 변수로, nums의 k번째 값으로 초기화한다.
- i는 좋은 부분 배열의 시작 위치를 저장할 변수로, $k - 1$를 넣고 i가 0 이상이면서 nums[i]의 값이 min 이상일 때 까지 i를 감소시키며 시작 위치를 초기화한다.
- j는 좋은 부분 배열의 종료 위치를 저장할 변수로, $k + 1$를 넣고 j가 length 미만이면서 nums[j]의 값이 min 이상일 때 까지 j를 증가시키며 종료 위치를 초기화한다.
- result는 최대 점수를 저장할 변수로, 현재 위치인 [i, j] 구간의 부분 배열의 점수인 $min \times (j - i - 1)$로 초기화한다.

3. i와 j가 배열 범위 내에 있을 때 까지 아래를 수행한다.
- i가 0 미만이거나 j가 length 미만이면서 nums[i]의 값이 nums[j]의 값 이하인 경우, min에 nums[j]의 값을 넣고 j가 length 미만이면서 min이 nums[j]의 값 이하일 때까지 j를 증가시킨다.
- 위의 경우가 아니라면, min에 nums[i]의 값을 넣고 i가 0 이상이면서 min이 nums[i]의 값 이하일 때 까지 i를 감소시킨다.
- 위의 수행이 완료되면 result에 result와 $min \times (j - i - 1)$ 중 큰 값을 넣어준다.

4. 반복이 완료되면 최대 점수인 result를 주어진 문제의 결과로 반환한다.

# 해설
- 첫 값부터 마지막 값까지 반복하여 각 수행에 따라 i와 j의 값을 증감시키므로 점수 계산 배율인 $j - i + 1$을 $(j - 1) - (i - 1) + 1 = j - i - 1$로 계산한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumScoreOfAGoodSubarray.java){:target="_blank"}에서 확인 가능합니다.