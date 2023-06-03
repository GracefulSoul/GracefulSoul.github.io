---
title: "Leetcode Java Time Needed to Inform All Employees"
excerpt: "Leetcode Time Needed to Inform All Employees Java"
last_modified_at: 2023-06-02T10:50:00
header:
  image: /assets/images/leetcode/time-needed-to-inform-all-employees.png
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
[Link](https://leetcode.com/problems/time-needed-to-inform-all-employees){:target="_blank"}

# 코드
```java
class Solution {

  public int numOfMinutes(int n, int headID, int[] manager, int[] informTime) {
    int result = 0;
    for (int i = 0; i < n; i++) {
      result = Math.max(result, this.dfs(manager, informTime, i));
    }
    return result;
  }

  private int dfs(int[] manager, int[] informTime, int i) {
    if (manager[i] != -1) {
      informTime[i] += this.dfs(manager, informTime, manager[i]);
      manager[i] = -1;
    }
    return informTime[i];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/time-needed-to-inform-all-employees/submissions/962671376/){:target="_blank"}

# 설명
1. [0, $n - 1$] 범위의 직원 ID가 존재하는데 사장 ID는 headID이며, 관리자들의 ID를 담은 manager와 전파하는데 걸리는 시간을 담은 informTime을 이용하여 사장이 모든 직원에게 전파하는데 걸리는 시간을 반환하는 문제이다.
- 단, manager[headID] = -1 이다.

2. result는 모든 직원에게 전파하는데 걸리는 시간을 담을 변수로, 0으로 초기화한다.

3. 0부터 n 미만까지 i를 증가시키며 아래를 수행한다.
- result에 result와 4번에서 정의한 dfs(int[] manager, int[] informTime, int i)를 수행한 결과 중 큰 값을 넣어준다.

4. DFS 방식으로 전파하는데 걸리는 시간을 구하기 위한 dfs(int[] manager, int[] informTime, int i) 메서드를 정의한다.
- manager의 i번째 값이 아닌 경우, 아래를 수행한다.
  - infromTime의 i번째 위치에 i번째 manager의 ID를 i에 넣어 재귀 호출한 결과를 넣어준다.
  - 전파 시간을 informTime에 넣었으므로, manager의 i번째 위치에 -1을 넣어 다음 호출에 무시하도록 처리한다.
- informTime의 i번째 값을 반환한다.

5. 전파하는데 걸리는 시간을 담은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TimeNeededToInformAllEmployees.java){:target="_blank"}에서 확인 가능합니다.