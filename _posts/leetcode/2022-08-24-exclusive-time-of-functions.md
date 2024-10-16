---
title: "Leetcode Java Exclusive Time of Functions"
excerpt: "Leetcode Exclusive Time of Functions Java"
last_modified_at: 2022-08-24T19:30:00
header:
  image: /assets/images/leetcode/exclusive-time-of-functions.png
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
[Link](https://leetcode.com/problems/exclusive-time-of-functions/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] exclusiveTime(int n, List<String> logs) {
    int[] result = new int[n];
    Stack<int[]> stack = new Stack<>();
    for (String log : logs) {
      String[] split = log.split(":");
      int id = Integer.valueOf(split[0]);
      int timestamp = Integer.valueOf(split[2]);
      if (split[1].equals("start")) {
        stack.push(new int[] { id, timestamp });
      } else {
        int time = timestamp - stack.pop()[1] + 1;
        result[id] += time;
        if (!stack.empty()) {
          result[stack.peek()[0]] -= time;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/782047437/){:target="_blank"}

# 설명
1. 단일 스레드의 CPU에서 0부터 $n - 1$의 고유한 아이디를 가지는 n개의 기능 별 수행 시간이 저장된 logs를 이용하여 id에 해당하는 크기의 배열의 각 자리에 맞추어 반환하는 문제이다.
- logs는 id, status(start OR end), timestamp를 콜론(":")을 사용해서 묶은 log들을 순차적으로 저장한 배열이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 각 기능의 수행 시간을 저장하기 위한 배열로, n의 크기로 초기화한다.
- stack은 로그를 이용하여 수행 내열을 저장하기 위한 변수로, Stack으로 정의한다.

3. logs의 모든 값들을 아래를 이용하여 반복 수행한다.
- log를 콜론(":")을 구분자로 나누어 split에 넣어준다.
- id에 split의 첫 번째 값을, timestamp에 split의 세 번째 값을 넣어준다.
- split의 두 번째 값이 "start"인 경우, stack에 id와 timestamp를 배열로 넣어 저장한다.
- split의 두 번째 값이 "end"인 경우 아래를 수행한다.
  - stack에서 저장한 값을 빼와 timestamp 차이를 계산해서 time에 넣어준다.
  - result의 id번째 값에 time을 더해준다.
  - stack이 비어있지 않은 경우 유휴 시간을 빼주어야 하므로, result의 stack의 다음 저장된 값의 id에 해당하는 값에 time을 빼준다.

4. 반복이 완료되면 각 기능 별 수행 시간을 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ExclusiveTimeOfFunctions.java){:target="_blank"}에서 확인 가능합니다.