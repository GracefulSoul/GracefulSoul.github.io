---
title: "Leetcode Java Largest Divisible Subset"
excerpt: "Leetcode Largest Divisible Subset Java 풀이"
last_modified_at: 2022-01-31T12:00:00
header:
  image: /assets/images/leetcode/largest-divisible-subset.png
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
[Link](https://leetcode.com/problems/largest-divisible-subset/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> largestDivisibleSubset(int[] nums) {
    int length = nums.length;
    int[][] dp = new int[length][2];
    Arrays.sort(nums);
    int max = 0;
    int index = -1;
    for (int i = 0; i < length; i++) {
      dp[i][0] = 1;
      dp[i][1] = -1;
      for (int j = 0; j < i; j++) {
        if (nums[i] % nums[j] == 0 && dp[j][0] + 1 > dp[i][0]) {
          dp[i][0] = dp[j][0] + 1;
          dp[i][1] = j;
        }
      }
      if (dp[i][0] > max) {
        max = dp[i][0];
        index = i;
      }
    }
    List<Integer> result = new ArrayList<Integer>();
    while (index != -1) {
      result.add(nums[index]);
      index = dp[index][1];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/631307010/){:target="_blank"}

# 설명
1. 주어진 정수 배열인 nums를 이용하여 아래의 조건을 만족하는 배열을 만드는 문제이다.
- 주어진 문제의 결과로 반환하는 answer에 들어가는 값들은 answer[i] % answer[j] == 0 혹은 answer[j] % answer[i] == 0을 만족해야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장하기 위한 변수로, nums.length로 초기화한다.
- dp는 주어진 문제의 조건에 해당하는 값을 찾기 위한 임시 배열로, 그 전의 위치를 순차적으로 담기 위해 dp[length][2]로 초기화한다.
- max는 최대 값을 저장하기 위한 임시 변수로, 0으로 초기화한다.
- index는 nums의 위치 값을 임시 저장하기 위한 임시 변수로, -1로 초기화 한다.

3. nums를 오름차순으로 정렬하고, nums의 모든 값을 앞에서부터 반복한다.
- dp[i][0]은 1로, dp[i][1]은 -1로 초기화 한다.
- 0부터 i까지 j를 증가시키며 반복하여, 아래를 검증하여 값을 설정한다.
  - nums[i]의 값과 nums[j]의 값의 나눈 나머지 값이 0이고 $dp[j][0] + 1$의 값이 dp[i][0]의 값보다 큰 경우, dp[i][0]에 dp[j][0] + 1 값을 dp[i][1]에 j를 넣어준다.
- dp[i][0]의 값이 max보다 큰 경우, max에 dp[i][0]의 값을 index에 i를 넣어주고 반복을 계속 수행한다.

4. 결과를 넣을 List인 result를 정의하고, index가 -1이 아닐 때 까지 반복한다.
- result에 조건을 만족하는 값인 nums의 index번째 값을 넣어주고, index에 이전의 값이 존재하는 위치인 dp[index][1] 값을 넣어준다.
- 최초 정의한 index인 -1이 되기 전까지 반복을 수행하여 조건에 만족하는 값들을 result에 모두 넣어준다.

5. 반복이 완료되면 문제의 조건을 만족하는 결과를 넣은 List인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestDivisibleSubset.java){:target="_blank"}에서 확인 가능합니다.