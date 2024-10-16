---
title: "Leetcode Java Total Cost to Hire K Workers"
excerpt: "Leetcode Total Cost to Hire K Workers Java"
last_modified_at: 2023-06-23T19:20:00
header:
  image: /assets/images/leetcode/total-cost-to-hire-k-workers.png
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
[Link](https://leetcode.com/problems/total-cost-to-hire-k-workers){:target="_blank"}

# 코드
```java
class Solution {

  public long totalCost(int[] costs, int k, int candidates) {
    long result = 0;
    if (candidates * 2 > costs.length - k || costs.length == k) {
      Arrays.sort(costs);
      for (int i = 0; i < k; i++) {
        result += costs[i];
      }
      return result;
    }
    int left = 0;
    int right = costs.length - 1;
    Queue<Integer> queue1 = new PriorityQueue<>();
    Queue<Integer> queue2 = new PriorityQueue<>();
    while (queue1.size() < candidates && left <= right) {
      queue1.offer(costs[left++]);
      queue2.offer(costs[right--]);
    }
    while (k-- > 0) {
      if (queue1.peek() <= queue2.peek()) {
        result += queue1.poll();
        queue1.offer(costs[left++]);
      } else {
        result += queue2.poll();
        queue2.offer(costs[right--]);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/total-cost-to-hire-k-workers/submissions/979933492/){:target="_blank"}

# 설명
1. costs의 값들 중 좌우의 candidates개 값들 중 가장 작은 값을 꺼내는 행위를 k번 반복했을 때, 꺼낸 값들의 합을 계산하는 문제이다.

2. result는 꺼낸 값들의 합을 저장할 변수로, 0으로 초기화한다.

3. 아래의 경우를 하나라도 만족하면 costs를 오름차순 정렬하여 앞의 k개의 값들을 result에 넣고 주어진 문제의 결과로 반환한다.
- candidates에 2를 곱한 결과가 cost의 길이에 k를 뺀 값보다 큰 경우, k번 수행하면서 모든 숫자를 다 검색하므로 가장 작은 값을 k개 꺼낸 것과 같다.
- costs의 길이가 k와 동일한 경우, 위와 유사하게 모든 값을 탐색하는 것과 같다,

4. 문제 풀이에 필요한 변수를 정의한다.
- left와 right는 좌측과 우측의 candidates개의 값을 유지하기 위한 위치 변수로, 0과 $costs.length - 1$로 초기화한다.
- queue1과 queue2는 좌측과 우측의 candidates개의 값을 저장하기 위한 변수로, 작은 값 순으로 정렬하여 보관하기 위해 PriorityQueue로 초기화한다.

5. queue1의 길이가 candidates보다 작고, left가 right보다 작거나 같을 때 까지 아래를 수행한다.
- queue1에 costs의 처음부터 candidates개의 값들을 차례대로 넣어준다.
- queue2에 costs의 마지막부터 candidates개의 값들을 차례대로 넣어준다.

6. k가 0보다 클 때 까지 아래를 수행하고 k를 감소시킨다.
- queue1의 가장 작은 값이 queue2의 가장 작은 값보다 작거나 같은 경우, 아래를 수행한다.
  - result에 queue1의 가장 작은 값을 꺼내 넣어준다.
  - queue1에 costs의 left번째 값을 넣어 candidates 크기로 유지하고, left를 증가시킨다.
- 위의 경우가 아니라면 아래를 수행한다.
  - result에 queue2의 가장 작은 값을 꺼내 넣어준다.
  - queue2에 costs의 right번째 값을 넣어 candidates 크기로 유지하고, right를 감소시킨다.

7. 반복이 완료되어 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TotalCostToHireKWorkers.java){:target="_blank"}에서 확인 가능합니다.