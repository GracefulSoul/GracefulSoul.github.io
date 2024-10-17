---
title: "Leetcode Java The Number of the Smallest Unoccupied Chair"
excerpt: "Leetcode Medium - 'The Number of the Smallest Unoccupied Chair' 문제 Java 풀이"
last_modified_at: 2024-10-11T22:00:00
header:
  image: /assets/images/leetcode/the-number-of-the-smallest-unoccupied-chair.png
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
[Link](https://leetcode.com/problems/the-number-of-the-smallest-unoccupied-chair/){:target="_blank"}

# 코드
```java
class Solution {

  public int smallestChair(int[][] times, int targetFriend) {
    int result = -1;
    int start = times[targetFriend][0];
    Arrays.sort(times, (x, y) -> x[0] - y[0]);
    Queue<int[]> queue = new PriorityQueue<>((x, y) -> x[0] - y[0]);
    Queue<Integer> chairs = new PriorityQueue<>();
    for (int i = 0, j = 0; i < times.length; i++) {
      while (!queue.isEmpty() && queue.peek()[0] <= times[i][0]) {
        chairs.offer(queue.poll()[1]);
      }
      result = chairs.isEmpty() ? j++ : chairs.poll();
      queue.offer(new int[] { times[i][1], result });
      if (times[i][0] == start) {
        break;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/the-number-of-the-smallest-unoccupied-chair/submissions/1419014746/){:target="_blank"}

# 설명
1. n명의 친구가 times의 순서대로 의자에 앉았다 일어날 때, targetFriend 번째 친구가 앉는 의자의 번호를 반환하는 문제이다.
- times[i] = [arrival<sub>i</sub>, leaving<sub>i</sub>]를 의미하며, arrival<sub>i</sub>는 앉는 시간 leaving<sub>i</sub>는 떠나는 시간을 뜻한다.
- targetFriend와 의자의 번호는 0-index이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 targetFriend 번째 친구가 앉는 의자의 번호를 저장할 변수로, -1로 초기화한다.
- start는 targetFriend 번째 친구가 앉기 시작하는 시간을 저장한 변수로, target[targetFriend][0]의 값으로 초기화한다.
- times는 의자에 앉는 시간 기준으로 오름차순 정렬한다.
- queue는 의자에서 떠나는 시간을 의자 번호와 같이 저장할 변수로, 떠나는 시간의 오름차순 정렬되는 PriorityQueue로 초기화한다.
- chairs는 앉아있는 의자를 저장할 변수로, 의자 순서대로 저장할 PriorityQueue로 초기화한다.

3. times탐색을 위한 위치인 i는 0부터 times 길이 미만까지 증가시키며, chairs가 비어있을 때 의자 시작 위치를 저장할 j는 0으로 초기화하여 아래를 수행한다.
- queue가 비어있지 않으면서 queue의 첫 친구가 의자에 앉는 시간이 times[i]의 의자에 앉는 시간 이하일 때까지, chairs에 queue에서 해당 친구가 의자를 떠나는 시간을 넣어준다.
- result에 chairs가 비어있으면 다음 의자인 j를 넣고 j를 증가시켜주고, 비어있지 않으면 chairs에서 현재 앉을 수 있는 의자를 배정시켜준다.
- queue에 i번째 친구가 의자를 떠나는 시간인 times[i][1]와 의자 번호인 result를 넣어준다.
- times[i][0]인 i번째 친구가 의자를 앉는 시간이 targetFriend 번째 친구가 앉는 시간인 start인 경우, 반복을 중지한다.

4. 위의 반복이 완료되면 의자의 번호가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TheNumberOfTheSmallestUnoccupiedChair.java){:target="_blank"}에서 확인 가능합니다.