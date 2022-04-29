---
title: "Leetcode Java Matchsticks to Square"
excerpt: "Leetcode Matchsticks to Square Java 풀이"
last_modified_at: 2022-04-29T13:00:00
header:
  image: /assets/images/leetcode/matchsticks-to-square.png
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
[Link](https://leetcode.com/problems/matchsticks-to-square/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean makesquare(int[] nums) {
    int sum = 0;
    for (int num : nums) {
      sum += num;
    }
    if (sum % 4 != 0) {
      return false;
    }
    Arrays.sort(nums);
    return this.dfs(nums, new boolean[nums.length], 0, sum / 4, 0, 1);
  }

  private boolean dfs(int[] nums, boolean[] dp, int curr, int target, int sum, int group) {
    if (group == 4) {
      return true;
    } else if (sum == target) {
      return this.dfs(nums, dp, 0, target, 0, group + 1);
    } else if (sum > target) {
      return false;
    } else {
      for (int idx = curr; idx < nums.length; idx++) {
        if (dp[idx] || (idx > 0 && nums[idx - 1] == nums[idx] && !dp[idx - 1])) {
          continue;
        }
        dp[idx] = true;
        if (this.dfs(nums, dp, idx + 1, target, sum + nums[idx], group)) {
          return true;
        }
        dp[idx] = false;
      }
      return false;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/689467874/){:target="_blank"}

# 설명
1. 성냥개비의 길이가 담긴 nums를 이용하여 정사각형을 만들 수 있는지 검증하는 문제이다.

2. nums 내 모든 값들을 sum에 더해서 넣어준다.

3. sum을 4로 나눈 나머지가 0이 아니면 정사각형을 만들 수 없으므로, false를 주어진 문제의 결과로 반환한다.

4. nums를 오름차순으로 정렬하고, 5번에서 정의한 dfs(int[] nums, boolean[] dp, int curr, int target, int sum, int group) 메서드로 정사각형을 만들 수 있는지 여부를 확인하여 해당 결과를 주어진 문제의 결과로 반환한다.

5. 정사각형을 만들 수 있는지 여부를 검증하기 위한 dfs(int[] nums, boolean[] dp, int curr, int target, int sum, int group) 메서드를 정의한다.
- group이 4인 경우 정사각형의 네 번째 변까지 완성 가능하므로, true를 반환한다.
- sum이 target인 경우 target 번째 변을 완성했으므로, group을 1 증가시켜서 재귀 호출을 수행한 결과를 반환한다.
- sum이 target보다 큰 경우 target번째 변이 다른 변보다 길어서 정사각형을 만들 수 없으므로, false를 반환한다.
- 그 외의 경우 curr부터 nums의 길이 미만까지 idx를 증가시키며 반복을 수행한다.
  - dp의 idx번째 값이 true이면 이미 검증된 항목이고, idx가 0 초과이며 nums의 $idx - 1$번째 값과 idx번째 값이 같으면서 dp의 $idx - 1$번째 값이 false인 경우 동일 값이 이어지므로 다음 반복을 수행한다.
  - 해당 위치를 다녀왔다는 의미로 dp의 idx번째 값을 true로 변경한다.
  - curr에 $idx + 1$ 값을 넣고, sum에 sum과 nums의 idx번째 값의 합을 넣고 재귀 호출을 수행한 결과가 true인 경우 정사각형을 만들 수 있으므로, true를 반환한다.
  - dp의 idx번째 값을 false로 다시 변경하여 다음 반복을 수행한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MatchsticksToSquare.java){:target="_blank"}에서 확인 가능합니다.