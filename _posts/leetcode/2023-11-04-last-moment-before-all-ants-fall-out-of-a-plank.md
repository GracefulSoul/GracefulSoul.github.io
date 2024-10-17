---
title: "Leetcode Java Last Moment Before All Ants Fall Out of a Plank"
excerpt: "Leetcode Medium - 'Last Moment Before All Ants Fall Out of a Plank' 문제 Java 풀이"
last_modified_at: 2023-11-04T17:00:00
header:
  image: /assets/images/leetcode/last-moment-before-all-ants-fall-out-of-a-plank.png
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
[Link](https://leetcode.com/problems/last-moment-before-all-ants-fall-out-of-a-plank){:target="_blank"}

# 코드
```java
class Solution {

  public int getLastMoment(int n, int[] left, int[] right) {
    int result = 0;
    for (int point : left) {
      result = Math.max(result, point);
    }
    for (int point : right) {
      result = Math.max(result, n - point);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/last-moment-before-all-ants-fall-out-of-a-plank/submissions/1091136476/){:target="_blank"}

# 설명
1. 널판지 위에 총 n마리의 개미 중 왼쪽으로 향하는 개미의 위치가 저장된 left와 오른쪽으로 향하는 개미의 위치가 저장된 right가 1초에 한 칸씩 이동할 때 모두 떨어지는데 걸리는 시간을 구하는 문제이다.

2. result는 개미가 널판지 위에서 모두 떨어지는 시간을 저장할 변수로, 0으로 초기화한다.

3. left의 값들 중 result에 가장 큰 값인 마지막으로 출발하는 개미의 위치를 넣어준다.

4. right의 값들 중 result에 가장 작은 값인 개미의 위치를 n에 뺀 값을 넣어준다.

5. 반복이 완료되면 가장 멀리 떨어진 개미가 널판지 아래로 떨어지는 시간이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LastMomentBeforeAllAntsFallOutOfAPlank.java){:target="_blank"}에서 확인 가능합니다.