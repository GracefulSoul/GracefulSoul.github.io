---
title: "Leetcode Java Task Scheduler"
excerpt: "Leetcode - 'Task Scheduler' 문제 Java 풀이"
last_modified_at: 2022-08-13T11:00:00
header:
  image: /assets/images/leetcode/task-scheduler.png
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
[Link](https://leetcode.com/problems/task-scheduler/){:target="_blank"}

# 코드
```java
class Solution {

  public int leastInterval(char[] tasks, int n) {
    int[] counts = new int[26];
    for (int task : tasks) {
      counts[task - 'A']++;
    }
    int max = 0;
    for (int count : counts) {
      max = Math.max(max, count);
    }
    int maxCount = 0;
    for (int count : counts) {
      if (count == max) {
        maxCount++;
      }
    }
    return Math.max(tasks.length, (max - 1) * (n + 1) + maxCount);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/772280399/){:target="_blank"}

# 설명
1. tasks를 이용하여 최소 n개의 유휴 시간을 이용해 작업을 아래의 조건을 만족하는 최소 단위의 수를 구하는 문제이다.
- tasks에 존재하는 영대문자는 각자 다른 작업을 의미한다.
- 유휴 시간의 전과 후는 동일한 작업을 수행해야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 tasks 내 각 작업의 개수를 저장할 변수로, tasks를 반복하여 count의 $task - 'A'$번째 값을 증가시킨다.
- max는 counts내 가장 큰 값을 저장할 변수로, counts를 반복하여 가장 큰 값을 max에 넣어준다.
- maxCount는 counts 내 max에 해당하는 작업의 개수를 저장할 변수로, counts를 반복하여 max와 동일한 횟수인 작업의 개수를 넣어준다.

3. tasks의 길이와 $(max - 1) \times (n + 1)$의 결과에 maxCount를 더한 결과 중 큰 값을 주어진 문제의 결과로 반환한다.
- 작업을 수행하는 최소 단위의 수는 tasks의 길이가 되므로, tasks의 길이와 비교한다.
- $(max - 1) \times (n + 1) + maxCount$은 아래를 뜻한다.
  - 최소 n개의 유휴 시간을 동일한 작업 사이에 넣어야 하므로, 부분 작업의 길이인 $max - 1$를 사용한다.
  - 최소 n개의 유휴 시간을 사용하여 작업을 수행하므로, 부분 작업의 수인 $n + 1$을 사용한다.
  - 두 경우를 곱하여 경우의 수를 구하고, 최대 작업의 수가 동일한 경우 바꿔 사용이 가능하므로 해당 개수를 더해준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TaskScheduler.java){:target="_blank"}에서 확인 가능합니다.