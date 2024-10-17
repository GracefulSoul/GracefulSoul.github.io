---
title: "Leetcode Java Find the Town Judge"
excerpt: "Leetcode Easy - 'Find the Town Judge' 문제 Java 풀이"
last_modified_at: 2023-09-30T10:20:00
header:
  image: /assets/images/leetcode/find-the-town-judge.png
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
[Link](https://leetcode.com/problems/find-the-town-judge){:target="_blank"}

# 코드
```java
class Solution {

  public int findJudge(int n, int[][] trust) {
    int[] count = new int[n + 1];
    for (int[] t : trust) {
      count[t[0]]--;
      count[t[1]]++;
    }
    for (int i = 1; i <= n; i++) {
      if (count[i] == n - 1) {
        return i;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-town-judge/submissions/1062678831/){:target="_blank"}

# 설명
1. n개의 [a, b]의 값이 있는 trust 배열 내 값으로 아래를 검증한 결과를 반환한다.
- a는 b를 가르키며, b의 값이 아무도 가르키지 않으면 해당 값을 반환한다.
- 위의 경우가 존재하지 않으면 -1을 반환한다.

2. count는 서로 연결되어 있는지 검증하기 위한 배열로, $n + 1$ 크기의 배열로 초기화한다.

3. trust의 모든 값을 반복하여 count의 첫 값에 해당하는 값은 감소, 두 번째 값에 해당하는 값은 증가시켜준다.

4. 1부터 n 이하까지 i를 증가시키며 count 값이 $n - 1$에 해당하면 해당 숫자를 모두 가르키므로 해당 값을 주어진 문제의 결과로 반환한다.

5. 반복이 완료되면 -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheTownJudge.java){:target="_blank"}에서 확인 가능합니다.