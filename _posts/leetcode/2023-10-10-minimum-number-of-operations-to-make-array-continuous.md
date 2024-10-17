---
title: "Leetcode Java Minimum Number of Operations to Make Array Continuous"
excerpt: "Leetcode Hard - 'Minimum Number of Operations to Make Array Continuous' 문제 Java 풀이"
last_modified_at: 2023-10-10T19:00:00
header:
  image: /assets/images/leetcode/minimum-number-of-operations-to-make-array-continuous.png
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
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-continuous){:target="_blank"}

# 코드
```java
class Solution {

  public int minOperations(int[] nums) {
    Arrays.sort(nums);
    int result = Integer.MAX_VALUE;
    int count = 0;
    int[] dp = new int[nums.length];
    for (int i = 0, j = 1; i < nums.length; i++) {
      while (j < nums.length && nums[j] <= nums[i] + nums.length - 1) {
        if (nums[j - 1] == nums[j]) {
          count++;
        }
        dp[j++] = count;
      }
      result = Math.min(result, i + (nums.length - j) + count - dp[i]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-continuous/submissions/1071703129/){:target="_blank"}

# 설명
1. nums 내 숫자들이 연속되도록 구성하고자할 때, 바꿀 최소 숫자의 갯수를 구하는 문제이다.

2. nums의 숫자들을 오름차순으로 정렬한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- result는 최소 숫자의 갯수를 저장할 변수로, 정수의 최댓값으로 초기화한다.
- count는 바꿀 숫자의 갯수를 계산할 변수로, 0으로 초기화한다.
- dp는 최소 숫자의 갯수를 계산하기 위한 배열로, nums의 길이 크기의 정수 배열로 초기화한다.

4. 0부터 nums의 길이 미만까지 i를 증가시키고 j는 1로 초기화 시켜 아래를 반복한다.
- j가 nums의 길이 미만이면서 nums[j]의 값이 $nums[i] + nums.length - 1$보다 같거나 작을 때 까지 아래를 반복한다.
  - nums의 $j - 1$번째 숫자와 j번째 숫자가 동일한 경우, 값을 바꿔야 하므로 count를 증가시킨다.
  - dp의 j번째 위치에 count를 넣어주고 j를 증가시킨다.
- result에 이전에 계산한 최소 갯수인 result와 $i + (nums.length - j) + count - dp[i]$인 [i, j] 사이 값을 정렬하고 다른 값을 변경할 경우 중 작은 값을 넣어준다.

5. 반복이 완료되면 최소 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumNumberOfOperationsToMakeArrayContinuous.java){:target="_blank"}에서 확인 가능합니다.