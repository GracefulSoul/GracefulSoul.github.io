---
title: "Leetcode Java Maximum Sum of Distinct Subarrays With Length K"
excerpt: "Leetcode - 'Maximum Sum of Distinct Subarrays With Length K' 문제 Java 풀이"
last_modified_at: 2024-11-19T18:30:00
header:
  image: /assets/images/leetcode/maximum-sum-of-distinct-subarrays-with-length-k.png
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
[Link](https://leetcode.com/problems/maximum-sum-of-distinct-subarrays-with-length-k/){:target="_blank"}

# 코드
```java
class Solution {

  public long maximumSubarraySum(int[] nums, int k) {
    boolean[] visited = new boolean[100001];
    long sum = 0L;
    long result = 0L;
    for (int i = 0, j = 0; j < nums.length; j++) {
      int num = nums[j];
      while (visited[num] || (j - i + 1 > k && i < j)) {
        sum -= nums[i];
        visited[nums[i++]] = false;
      }
      sum += num;
      if (j - i + 1 == k) {
        result = Math.max(result, sum);
      }
      visited[num] = true;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-sum-of-distinct-subarrays-with-length-k/submissions/1457096839/){:target="_blank"}

# 설명
1. nums와 k를 이용하여 아래의 조건을 만족하는 가능한 부분 배열의 합이 최대인 값을 구하는 문제이다.
- 부분 배열의 크기는 k이다.
- 모든 요소는 동일한 값이 존재하지 않는다.
- 위 두 조건을 만족하는 부분 배열이 없는 경우, 0을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- visited는 방문한 값을 체크하기 위한 변수로, 값의 최대 가능한 범위인 $10^5$보다 1 큰 크기의 부울 배열로 초기화한다.
- sum은 합계를 계산하기 위한 변수로, 0으로 초기화한다.
- result는 조건을 만족하는 합이 최대인 값을 저장할 변수로, 0으로 초기화한다.

3. i는 0부터, j는 0부터 nums의 길이 미만까지 j를 증가시키면서 아래를 반복한다.
- num에 nums[j]의 값을 저장한다.
- visited[num]이 true인 사용한 값인 경우이거나, $j - i + 1$이 k를 초과하면서 i가 j 미만일 때 까지 sum에 nums[i]의 값을 빼주고, visited[nums[i]]의 값을 false로 바꾼 뒤 i를 증가시켜준다.
- sum에 num을 더해 현재 위치의 값을 더해준다.
- $j - i + 1$이 k인 부분 배열 크기에 만족하면, result에 result와 sum 중 큰 값을 넣어준다.
- visited[num]에 true를 넣어 사용한 값을 체크해준다.

4. 반복이 완료되면 최대 합계가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumSumOfDistinctSubarraysWithLengthK.java){:target="_blank"}에서 확인 가능합니다.