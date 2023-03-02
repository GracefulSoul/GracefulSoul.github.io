---
title: "Leetcode Java Mirror Reflection"
excerpt: "Leetcode Mirror Reflection Java"
last_modified_at: 2023-03-02T19:40:00
header:
  image: /assets/images/leetcode/mirror-reflection.png
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
[Link](https://leetcode.com/problems/mirror-reflection){:target="_blank"}

# 코드
```java
class Solution {

  public int mirrorReflection(int p, int q) {
    while (p % 2 == 0 && q % 2 == 0) {
      p /= 2;
      q /= 2;
    }
    return 1 - (p % 2) + (q % 2);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/mirror-reflection/submissions/907663037/){:target="_blank"}

# 설명
1. 한 변의 길이가 p인 거울로 이루어진 사면체 내에서 남서쪽에서 발사된 레이저가 아래의 수용체 중 먼저 도달하는 지점을 구하는 문제이다.
- 레이저가 발사되는 남서쪽의 모서리를 제외하고 우측부터 위, 좌측 순으로 0, 1, 2의 수용체가 존재한다.
- 레이저는 남서쪽 모서리에서 남동쪽 0 수용체 위의 q 거리로 발사된다.

2. p와 q를 가자 2로 나눈 값이 모두 0일 때까지 아래를 수행한다.
- p와 q를 각자 2로 나눈 값을 넣어준다.

3. 2번이 반복이 완료되면 1에서 p에서 2를 나눈 나머지를 빼고 q에서 2를 나눈 나머지를 더한 결과를 주어진 문제의 결과로 반환한다.
- p가 홀수이고 q가 짝수인 경우 한 바퀴 돌아서, 0 수용체에 도달한다.
- p가 짝수이고 q가 홀수인 경우 좌우 벽에 반사되어, 2 수용체에 도달한다.
- p와 q가 홀수인 경우 좌우 벽에 반사되어, 1 수용체에 도달한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MirrorReflection.java){:target="_blank"}에서 확인 가능합니다.