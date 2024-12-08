---
title: "Leetcode Java Two Best Non-Overlapping Events"
excerpt: "Leetcode - 'Two Best Non-Overlapping Events' 문제 Java 풀이"
last_modified_at: 2024-12-08T12:20:00
header:
  image: /assets/images/leetcode/two-best-non-overlapping-events.png
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
[Link](https://leetcode.com/problems/two-best-non-overlapping-events/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxTwoEvents(int[][] events) {
    Arrays.sort(events, (a, b) -> a[0] == b[0] ? a[1] - b[1] : a[0] - b[0]);
    Queue<int[]> queue = new PriorityQueue<>((a, b) -> a[0] - b[0]);
    int max = 0;
    int result = 0;
    for (int[] event : events) {
      int start = event[0];
      while (!queue.isEmpty() && queue.peek()[0] < start) {
        max = Math.max(max, queue.remove()[1]);
      }
      result = Math.max(result, event[2] + max);
      queue.add(new int[] { event[1], event[2] });
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/two-best-non-overlapping-events/submissions/1473115722/){:target="_blank"}

# 설명
1. 아래의 구성으로 된 events를 이용하여 중첩되지 않은 event로 구성된 value 값의 합이 최대인 조합을 찾는 문제이다.
- events[i] = [start<sub>i</sub>, end<sub>i</sub>, value<sub>i</sub>]로 구성되어있다.

2. events를 시작 시간과 종료 시간에 대한 순차적인 오름차순으로 정렬해준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- queue는 시작 시간 별 정렬된 값들을 저장할 변수로, PriorityQueue로 초기화한다.
- max는 중첩된 events 중 가장 큰 value를 저장할 변수로, 0으로 초기화한다.
- result는 value 합이 최대인 결과를 저장하기 위한 변수로, 0으로 초기화한다.

4. events를 순차적으로 event에 넣어 아래를 수행한다.
- start에 event[0]의 값을 넣어준다.
- queue가 비어있지 않거나 queue의 첫 값의 종료 시간이 start 이하인 경우, max에 max와 queue의 값을 꺼낸 후 해당 value 중 큰 값을 넣어준다.
- result에 이전까지 최대 값인 result와 $event[2] + max$인 두 event의 value 합 중 큰 값을 넣어준다.
- queue에 종료시간과 value인 [event[1], event[2]]의 값을 배열로 넣어준다.

5. 반복이 완료되면 value 값의 합이 최대가 되는 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TwoBestNonOverlappingEvents.java){:target="_blank"}에서 확인 가능합니다.