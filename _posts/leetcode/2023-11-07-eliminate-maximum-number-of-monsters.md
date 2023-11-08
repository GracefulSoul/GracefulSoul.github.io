---
title: "Leetcode Java Eliminate Maximum Number of Monsters"
excerpt: "Leetcode Eliminate Maximum Number of Monsters Java"
last_modified_at: 2023-11-07T19:00:00
header:
  image: /assets/images/leetcode/eliminate-maximum-number-of-monsters.png
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
[Link](https://leetcode.com/problems/eliminate-maximum-number-of-monsters){:target="_blank"}

# 코드
```java
class Solution {

  public int eliminateMaximum(int[] dist, int[] speed) {
    int length = dist.length;
    for (int i = 0; i < length; i++) {
      dist[i] = (dist[i] - 1) / speed[i];
    }
    Arrays.sort(dist);
    for (int i = 0; i < length; i++) {
      if (dist[i] < i) {
        return i;
      }
    }
    return length;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/eliminate-maximum-number-of-monsters/submissions/1093510343/){:target="_blank"}

# 설명
1. dist 거리에 있는 괴물들이 speed의 속도로 달려올 때, 1분에 한 번씩 쏠 수 있는 총으로 잡을 수 있는 괴물의 최대 수를 구하는 문제이다.

2. length는 dist의 길이인 괴물의 수를 저장할 변수이다.

3. 0부터 length 미만까지 i를 증가시키면서 dist[i]에 $\frac{dist[i] - 1}{spped[i]}$인 몬스터가 도달하는 시간을 저장해준다.

4. dist를 오름차순 정렬해준 후 dist[i]가 i보다 작은 경우, 몬스터가 해당 시간 이전에 도달했으므로 i를 주어진 문제의 결과로 반환한다.

5. 반복이 완료되면 모든 괴물을 잡았으므로 length를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EliminateMaximumNumberOfMonsters.java){:target="_blank"}에서 확인 가능합니다.