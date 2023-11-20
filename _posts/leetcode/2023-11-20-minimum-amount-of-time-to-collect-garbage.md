---
title: "Leetcode Java Minimum Amount of Time to Collect Garbage"
excerpt: "Leetcode Minimum Amount of Time to Collect Garbage Java"
last_modified_at: 2023-11-20T18:40:00
header:
  image: /assets/images/leetcode/minimum-amount-of-time-to-collect-garbage.png
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
[Link](https://leetcode.com/problems/minimum-amount-of-time-to-collect-garbage){:target="_blank"}

# 코드
```java
class Solution {

  public int garbageCollection(String[] garbage, int[] travel) {
    int[] charArray = new int[128];
    char[] garbages = new char[] { 'M', 'P', 'G' };
    int result = 0;
    for (int i = 0; i < garbage.length; i++) {
      result += garbage[i].length();
      for (int j = 0; j < garbage[i].length(); j++) {
        charArray[garbage[i].charAt(j)] = i;
      }
    }
    for (int i = 1; i < travel.length; i++) {
      travel[i] += travel[i - 1];
    }
    for (int g : garbages) {
      if (charArray[g] > 0) {
        result += travel[charArray[g] - 1];
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reduction-operations-to-make-the-array-elements-equal/submissions/1102630400/){:target="_blank"}

# 설명
1. 철, 종이, 유리 쓰레기를 순차적으로 'M', 'P', 'G' 문자로 정의하고 각각 걸리는 시간을 travel로 정의할 때, garbage의 모든 쓰레기를 수거하기 위한 시간을 계산하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 쓰레기를 저장하기 위한 변수로, 영대문자의 최대 ASCII 코드 값인 128 크기의 정수 배열로 초기화한다.
- garbages는 쓰레기인 'M', 'P', 'G' 문자를 저장한 배열이다.
- result는 수거하는데 걸리는 시가을 저장하기 위한 변수로, 0으로 초기화한다.

3. 0부터 garbage의 크기 미만까지 i를 증가시키며 아래를 반복한다.
- result에 garbage의 크기를 더해준다.
- 0부터 garbage[i]의 길이 미만까지 j를 증가시키며, charArray 내 garbage[i]의 j번째 문자 위치에 마지막 발생한 위치인 i를 넣어준다.

4. 1부터 travel 길이 미만까지 travel[i]에 travel[$i - 1$]을 더해 시간을 더해준다.

5. garbages를 순차적으로 g에 넣어 charArray[g]의 값이 0보다 큰 경우, result에 travel의 $charArray[g] - 1$인 소요 시간을 더해준 후 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumAmountOfTimeToCollectGarbage.java){:target="_blank"}에서 확인 가능합니다.