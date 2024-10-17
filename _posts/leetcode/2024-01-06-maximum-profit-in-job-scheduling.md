---
title: "Leetcode Java Maximum Profit in Job Scheduling"
excerpt: "Leetcode Hard - 'Maximum Profit in Job Scheduling' 문제 Java 풀이"
last_modified_at: 2024-01-06T12:30:00
header:
  image: /assets/images/leetcode/maximum-profit-in-job-scheduling.png
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
[Link](https://leetcode.com/problems/maximum-profit-in-job-scheduling){:target="_blank"}

# 코드
```java
class Solution {

  public int jobScheduling(int[] startTime, int[] endTime, int[] profit) {
    int length = startTime.length;
    Job[] jobs = new Job[length];
    for (int i = 0; i < length; i++) {
      jobs[i] = new Job(startTime[i], endTime[i], profit[i]);
    }
    Arrays.sort(jobs, Comparator.comparingInt(a -> a.end));
    return this.jobScheduling(jobs, new int[length]);
  }

  private int jobScheduling(Job[] jobs, int[] dp) {
    int length = jobs.length;
    dp[0] = jobs[0].profit;
    for (int i = 1; i < length; i++) {
      int profit = jobs[i].profit;
      int index = this.search(jobs, i);
      if (index != -1) {
        profit += dp[index];
      }
      dp[i] = Math.max(profit, dp[i - 1]);
    }
    return dp[length - 1];
  }

  private int search(Job[] jobs, int index) {
    int start = 0, end = index - 1;
    while (start <= end) {
      int mid = start + ((end - start) / 2);
      if (jobs[index].start >= jobs[mid + 1].end) {
        start = mid + 1;
      } else if (jobs[index].start >= jobs[mid].end) {
        return mid;
      } else {
        end = mid - 1;
      }
    }
    return -1;
  }
}

class Job {

  int start;
  int end;
  int profit;

  public Job(int start, int end, int profit) {
    this.start = start;
    this.end = end;
    this.profit = profit;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-profit-in-job-scheduling/submissions/1138119137/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 job을 이용하여 겹치지 않도록 작업을 수행할 때, 얻을 수 있는 최대 이익을 반환하는 문제이다.
- i번째 작업인 job[i]는 [startTime[i], endTime[i]]동안 수행한 작업의 이윤이 profit[i]이라는 의미이다.
- endTime과 startTime이 동일한 다른 작업의 경우, 바로 다음 작업을 수행할 수 있다.

2. 작업에 대한 start, end, proift 정보를 같이 관리하기 위한 Job 클래스를 정의한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- length는 startTime의 길이를 저장한 변수이다.
- jobs는 각 작업 정보를 저장하기 위한 Job 배열로, 0부터 length까지 반복하여 각 작업 정보를 jobs에 순차적으로 같이 넣어준 후 종료 시간 기준으로 정렬해준다.
- 4번에서 정의한 jobScheduling(Job[] jobs, int[] dp) 메서드를 dp 자리에 length 크기의 정수 배열을 초기화해 넣어 수행한 결과를 주어진 문제의 결과로 반환한다.

4. 작업의 최대 이익을 계산하기 위한 jobScheduling(Job[] jobs, int[] dp) 메서드를 정의한다.
- length에 jobs의 길이를 저장한다.
- dp의 첫 자리에 가장 짧게 종료되는 jobs[0]의 profit 값을 넣어준다.
- 1부터 length 미만까지 i를 증가시키며 아래를 반복한다.
  - profit에 jobs[i]의 profit 값을 넣어준다.
  - index에 5번에서 정의한 search(Job[] jobs, int index) 메서드를 index자리에 i를 넣어 수행한 결과를 넣어준다.
  - index가 -1이면 현재 작업을 이어 수행할 수 있으므로, profit에 이전까지 이익의 합계인 dp[index]의 값을 더해준다.
  - dp[i]의 자리에 profit과 dp[$i - 1$]의 값 중 최대 이익이 되는 값을 넣어준다.
- 반복이 완료되면 최대 이익이 계산된 dp[$length - 1$]을 주어진 문제의 결과로 반환한다.

5. 작업 시간이 겹치는지 검사할 search(Job[] jobs, int index) 메서드를 정의한다.
- start에 0을, end에 $index - 1$인 이전까지 위치를 넣어준다.
- start가 end 이하일 때까지 아래를 반복한다.
  - mid에 $start + \frac{end - start}{2}$의 중앙값을 넣어준다.
  - jobs[index].start의 값이 jobs[$mid + 1$].end의 값보다 크거나 같으면, start에 $mid + 1$을 넣어 시작 위치를 증가시켜준다.
  - 위를 만족하지 않고 jobs[index].start의 값이 jobs[mid].end의 값보다 크거나 같으면, mid를 반환한다.
  - 위의 모든 값을 만족하지 않으면 end에 $mid - 1$을 넣어 종료 위치를 감소시켜준다.
- 반복이 완료되면 겹치는 시간이 존재하지 않으므로 -1을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumProfitInJobScheduling.java){:target="_blank"}에서 확인 가능합니다.