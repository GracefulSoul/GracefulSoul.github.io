---
title: "Leetcode Java Teemo Attacking"
excerpt: "Leetcode Teemo Attacking Java 풀이"
last_modified_at: 2022-05-16T09:00:00
header:
  image: /assets/images/leetcode/teemo-attacking.png
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
[Link](https://leetcode.com/problems/teemo-attacking/){:target="_blank"}

# 코드
```java
class Solution {

  public int findPoisonedDuration(int[] timeSeries, int duration) {
    int result = 0;
    int start = 0;
    int end = -1;
    for (int time : timeSeries) {
      if (end < time) {
        result += end - start + 1;
        start = time;
      }
      end = time + duration - 1;
    }
    return result + end - start + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/700334106/){:target="_blank"}

# 설명
1. duration 동안 중독되는 독 공격 횟수 별 시간인 timeSeries가 주어지면 겹치지 않은 중독된 시간을 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 총 중독된 시간을 계산할 변수로, 0으로 초기화한다.
- start는 중독된 시간을 계산하기 위한 시작 시간을 저장할 변수로, 0으로 초기화한다.
- end는 중독된 시간을 계산하기 위한 종료 시간을 저장할 변수로, start보다 작게 -1로 초기화한다.

3. timeSeries의 모든 값을 반복하여 중독된 시간을 계산한다.
- end가 time보다 작으면 겹치지 않은 시간의 중독이므로, result에 중독된 시간인 $end - start + 1$를 더해주고 start에 time을 넣어준다.
- end에 time에 중독이 발생하면 끝나는 시간인 $time + duration - 1$을 넣어주고 반복을 계속 한다.

4. 반복이 종료되면 중복되지 않은 중독된 시간으로 계산된 result와 마지막으로 중독된 시간인 $end - start + 1$을 더한 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TeemoAttacking.java){:target="_blank"}에서 확인 가능합니다.