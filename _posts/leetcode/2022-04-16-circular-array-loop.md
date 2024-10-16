---
title: "Leetcode Java Circular Array Loop"
excerpt: "Leetcode Circular Array Loop Java 풀이"
last_modified_at: 2022-04-16T13:00:00
header:
  image: /assets/images/leetcode/circular-array-loop.png
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
[Link](https://leetcode.com/problems/circular-array-loop/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean circularArrayLoop(int[] nums) {
    int[] visited = new int[nums.length];
    for (int idx = 0; idx < nums.length; idx++) {
      if (visited[idx] == 0 && this.dfs(nums, visited, idx)) {
        return true;
      }
    }
    return false;
  }

  private boolean dfs(int[] nums, int[] visited, int start) {
    if (visited[start] == 2) {
      return false;
    }
    visited[start] = 1;
    int next = (start + nums[start]) % nums.length;
    if (next < 0) {
      next += nums.length;
    }
    if (next == start || nums[next] * nums[start] < 0) {
      visited[start] = 2;
      return false;
    } else if (visited[next] == 1) {
      visited[start] = 2;
      return true;
    } else if (this.dfs(nums, visited, next)) {
      return true;
    } else {
      visited[start] = 2;
      return false;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/681221745/){:target="_blank"}

# 설명
1. 정수 배열인 nums를 이용하여 아래의 규칙으로 배열 내 값들을 계속 순회할 수 있는지 검증하는 문제이다.
- nums[i]가 양수이면 nums[i] 값 만큼 앞으로 이동한다.
- nums[i]가 음수이면 nums[i] 값 만큼 뒤로 이동한다.
- 위의 규칙대로 수행하여 시퀀스는 seq[0] -> seq[1] -> ... -> seq[k - 1] -> seq[0] -> ... 형태로 반복이 되어야 한다.

2. visited 배열을 nums의 길이만큼의 정수 배열로 초기화한다.

3. 0부터 nums의 길이 미만까지 idx를 증가시키며 visited의 idx번째 값이 0이고, 4번에서 정의한 dfs(int[] nums, int[] visited, int start) 메서드의 결과가 true이면 주어진 문제의 결과로 true를 반환한다.

4. nums 내 요소들을 이용하여 검증을 수행할 dfs(int[] nums, int[] visited, int start) 메서드를 정의한다.
- visited의 start번째 값이 2인 경우, 이미 검증한 단계이므로 false를 반환한다.
- visited의 start번째 값에 검증을 진행하고 있다는 의미로 1을 넣어준다.
- next에 $start + nums[start]$의 값에서 nums의 길이만큼 나눈 나머지 값을 넣어주고, next가 0 미만인 경우 nums.length를 추가해준다.
- next가 start와 동일하거나 nums의 next번째 값과 nums의 start번째 값의 곱이 0 미만인 경우, visited의 start번째 값을 2로 넣어주고 false를 반환한다.
  - nums의 next번째 값과 nums의 start번째 값의 곱이 0 미만인 음수인 경우는 next번째 위치와 start번째 위치를 번갈아 이동하므로 순회한다고 볼 수 없다.
- visited의 next번째 값이 1인 경우 visited의 start번째 값을 2로 넣어주고 true를 반환한다.
  - 위의 경우가 아니면 정상적으로 순회하는 경우이다.
- next의 값을 이용해 재귀 호출한 결과가 true인 경우, true를 반환한다.
  - 현재 위치까지는 순회하지 않지만, next의 값에서 순회하는 경우이다.
- 그 외의 경우 visited의 start번째 값을 2로 바꿔주고 false를 반환한다.
  - 그 외의 경우 순회하는 경우가 아니다.

5. 반복이 완료되면 각 요소를 이용하여 사이클이 이루어지지 않으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CircularArrayLoop.java){:target="_blank"}에서 확인 가능합니다.