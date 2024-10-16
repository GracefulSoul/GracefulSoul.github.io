---
title: "Leetcode Java The Number of Beautiful Subsets"
excerpt: "Leetcode The Number of Beautiful Subsets Java"
last_modified_at: 2024-05-23T20:00:00
header:
  image: /assets/images/leetcode/the-number-of-beautiful-subsets.png
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
[Link](https://leetcode.com/problems/the-number-of-beautiful-subsets/){:target="_blank"}

# 코드
```java
class Solution {

  public int beautifulSubsets(int[] nums, int k) {
    Arrays.sort(nums);
    return this.dfs(nums, k, new int[1001], 0, 0);
  }

  private int dfs(int[] nums, int k, int[] counts, int i, int count) {
    for (int j = i; j < nums.length; j++) {
      if (nums[j] <= k || counts[nums[j] - k] == 0) {
        counts[nums[j]]++;
        count = this.dfs(nums, k, counts, j + 1, count + 1);
        counts[nums[j]]--;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/the-number-of-beautiful-subsets/submissions/1265718820/){:target="_blank"}

# 설명
1. nums를 이용한 부분 배열 내 값들 중 값의 차이가 k가 되지 않는 부분 배열의 갯수를 구하는 문제이다.

2. num의 값들을 오름차순으로 정렬한 후 3번에서 정의한 dfs(int[] nums, int k, int[] counts, int i, int count) 메서드를 counts에 값의 최대 크기보다 1 큰 1001을, i와 count에 0을 넣어 수행한 결과를 주어진 문제의 결과로 반환한다.

3. DFS 방식으로 부분 배열의 갯수를 계산할 dfs(int[] nums, int k, int[] counts, int i, int count) 메서드를 정의한다.
- i부터 nums의 길이 미만까지 j를 증가시키며 아래를 반복한다.
  - nums[j]의 값이 k보다 작은 비교가 불가능하거나, $counts[nums[j] - k]$인 nums[j]의 값보다 k 작은 값의 갯수가 0이면 다음을 수행한다.
  - counts[nums[j]]의 값을 증가시켜 부분 배열의 갯수를 증가시켜준다.
  - count에 i 자리에 $j + 1$을, count 자리에 $count + 1$을 넣어 재귀 호출한 결과를 넣어준다.
  - counts[nums[j]]의 값을 감소시켜, 위에서 계산한 경우에 대해서 원복해준다.
- 반복이 완료되면 계산된 부분 배열의 수인 count를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TheNumberOfBeautifulSubsets.java){:target="_blank"}에서 확인 가능합니다.