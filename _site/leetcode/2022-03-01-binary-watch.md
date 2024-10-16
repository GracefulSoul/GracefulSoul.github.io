---
title: "Leetcode Java Binary Watch"
excerpt: "Leetcode Binary Watch Java 풀이"
last_modified_at: 2022-03-01T15:00:00
header:
  image: /assets/images/leetcode/binary-watch.png
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
[Link](https://leetcode.com/problems/binary-watch/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> readBinaryWatch(int turnedOn) {
    List<String> times = new ArrayList<String>();
    for (int hour = 0; hour < 12; hour++) {
      for (int minute = 0; minute < 60; minute++) {
        int bits = Integer.bitCount(hour) + Integer.bitCount(minute);
        if (bits == turnedOn) {
          times.add(this.getTime(hour, minute));
        }
      }
    }
    return times;
  }

  private String getTime(int hour, int minute) {
    return new StringBuilder().append(hour).append(":").append(minute / 10).append(minute % 10).toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/651045172/){:target="_blank"}

# 설명
1. 1부터 10까지 임의의 숫자인 turnedOn이 주어지면, 바이너리 워치에서 표현 가능한 시간을 반환하는 문제이다.
- 바이너리 워치는 상단에 시간을 나타내는 4개(8, 4, 2, 1)의 숫자와 하단에 분을 나타내는 6개(32, 16, 8, 4, 2 , 1)의 숫자가 존재한다.
- 시간은 앞 자리에 0을 넣지 않고, 분은 앞 자리에 0을 넣어 시간 표현식을 만들어 준다.
- 예를 들어, "01:00"와 "10:2"는 유효하지 않고, "1:00"와 "10:02"는 유효하다.

2. 결과를 넣을 times를 ArrayList로 초기화 한다.

3. 0부터 11까지 hour를 증가시키며 반복한다.
- 0부터 59까지 minute를 증가시키며 반복을 수행한다.
  - hour와 minute의 이진 표현에 있는 비트 수의 합이 turnedOn과 동일한 경우, hour와 minute를 주어진 시간 표현식에 맞춰 변환하여 times에 넣어준다.

4. 반복이 완료되면 표현 가능한 시간을 저장한 times를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryWatch.java){:target="_blank"}에서 확인 가능합니다.