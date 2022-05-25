---
title: "Leetcode Java Relative Ranks"
excerpt: "Leetcode Relative Ranks Java"
last_modified_at: 2022-05-25T13:00:00
header:
  image: /assets/images/leetcode/relative-ranks.png
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
[Link](https://leetcode.com/problems/relative-ranks/){:target="_blank"}

# 코드
```java
class Solution {

  public String[] findRelativeRanks(int[] score) {
    int length = score.length;
    int max = 0;
    for (int s : score) {
      if (s > max) {
        max = s;
      }
    }
    int[] map = new int[max + 1];
    for (int idx = 0; idx < length; idx++) {
      map[score[idx]] = idx + 1;
    }
    String[] result = new String[length];
    int count = 0;
    for (int idx = max; idx >= 0; idx--) {
      if (map[idx] != 0) {
        switch (++count) {
          case 1: result[map[idx] - 1] = "Gold Medal"; break;
          case 2: result[map[idx] - 1] = "Silver Medal"; break;
          case 3: result[map[idx] - 1] = "Bronze Medal"; break;
          default: result[map[idx] - 1] = String.valueOf(count);
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/706588616/){:target="_blank"}

# 설명
1. 점수를 담은 score를 이용하여 1위는 "Gold Medal", 2위는 "Silver Medal", 3위는 "Bronze Medal", 그 외는 각자 등수를 담은 배열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 score의 길이를 저장할 변수이다.
- max는 score 내 가장 큰 점수를 저장할 변수로, score를 반복하여 최댓값을 넣어준다.
- map은 각 점수 별 위치를 저장할 배열로, $max + 1$ 크기로 정의하고 score를 반복하여 해당 점수에 해당하는 위치에 $idx + 1$을 넣어준다.
- result는 결과를 넣어줄 배열로, length의 크기만한 문자열 배열로 정의한다.
- count는 등수를 계산할 변수로, 0으로 초기화한다.

3. max부터 0까지 idx를 감소시키며 반복하여 아래를 수행한다.
- map의 idx번째 값이 0이 아닌 경우 score에 존재하는 값으로, 아래의 절차대로 result에 값을 넣어준다.
  - count를 증가시킨 값이 1인 경우, result의 $map[idx] - 1$번째 위치에 "Gold Medal"을 넣어준다.
  - count를 증가시킨 값이 2인 경우, result의 $map[idx] - 1$번째 위치에 "Silver Medal"을 넣어준다.
  - count를 증가시킨 값이 3인 경우, result의 $map[idx] - 1$번째 위치에 "Bronze Medal"을 넣어준다.
  - count를 증가시킨 값이 4 이상인 경우, result의 $map[idx] - 1$번째 위치에 count를 넣어준다.

4. 반복이 완료되면 결과를 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RelativeRanks.java){:target="_blank"}에서 확인 가능합니다.