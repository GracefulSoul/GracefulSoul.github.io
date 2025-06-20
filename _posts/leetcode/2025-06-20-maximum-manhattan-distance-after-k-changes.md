---
title: "Leetcode Java Maximum Manhattan Distance After K Changes"
excerpt: "Leetcode - 'Maximum Manhattan Distance After K Changes' 문제 Java 풀이"
last_modified_at: 2025-06-20T20:40:00
header:
  image: /assets/images/leetcode/maximum-manhattan-distance-after-k-changes.png
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
[Link](https://leetcode.com/problems/maximum-manhattan-distance-after-k-changes/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxDistance(String s, int k) {
    char[] charArray = s.toCharArray();
    int[] position = new int[2];
    int result = 0;
    for (int i = 0; i < charArray.length; i++) {
      switch (charArray[i]) {
        case 'N': position[1]++; break;
        case 'S': position[1]--; break;
        case 'E': position[0]++; break;
        default: position[0]--; break;
      }
      int distance = Math.abs(position[0]) + Math.abs(position[1]);
      result = Math.max(result, distance + Math.min(2 * k, i + 1 - distance));
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-manhattan-distance-after-k-changes/submissions/1670472874/){:target="_blank"}

# 설명
1. 아래 규칙대로 이동하는 문자들이 저장된 s를 이용하여 순차적으로 이동할 때, 최대 k개의 문자를 변환하여 최대 이동 거리를 반환하는 문제이다.
- 'N'은 북쪽으로 1 이동한다.
- 'S'는 남쪽으로 1 이동한다.
- 'E'은 동쪽으로 1 이동한다.
- 'W'은 서쪽으로 1 이동한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 s를 문자 배열로 변환한 변수이다.
- position은 이동 위치를 저장할 변수로, 2 크기의 정수 배열로 초기화한다.
- result는 최대 이동 거리를 저장할 변수로, 0으로 초기화한다.

3. 0부터 charArray의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- charArray[i] 문자에 따라 아래를 수행한다.
  - 'N' 문자인 경우, position[1]의 값인 y축 값을 증가시켜준다.
  - 'S' 문자인 경우, position[1]의 값인 y축 값을 감소시켜준다.
  - 'E' 문자인 경우, position[0]의 값인 x축 값을 증가시켜준다.
  - 그 외인 'S' 문자인 경우, position[0]의 값인 x축 값을 감소시켜준다.
- distance는 x축과 y축의 값인 position[0]과 position[1]의 값의 절댓값의 합을 더해준다.
- result에 result와 distance에 이동 횟수를 변경하여 이동 가능한 최대 거리인 $2 \times k$와 가능한 최대 거리를 도달하기 위한 남은 거리인 $i + 1 - distance$ 중 작은 값을 넣어준다.

4. 반복이 완료되면 최대 이동 거리가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumManhattanDistanceAfterKChanges.java){:target="_blank"}에서 확인 가능합니다.