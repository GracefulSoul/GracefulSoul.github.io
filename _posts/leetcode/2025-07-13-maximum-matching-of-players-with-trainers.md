---
title: "Leetcode Java Maximum Matching of Players With Trainers"
excerpt: "Leetcode - 'Maximum Matching of Players With Trainers' 문제 Java 풀이"
last_modified_at: 2025-07-13T13:30:00
header:
  image: /assets/images/leetcode/maximum-matching-of-players-with-trainers.png
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
[Link](https://leetcode.com/problems/maximum-matching-of-players-with-trainers/){:target="_blank"}

# 코드
```java
class Solution {

  public int matchPlayersAndTrainers(int[] players, int[] trainers) {
    Arrays.sort(players);
    Arrays.sort(trainers);
    int i = 0;
    int j = 0;
    int result = 0;
    while (j < trainers.length && i < players.length) {
      if (players[i] > trainers[j]) {
        while (j < trainers.length && trainers[j] < players[i]) {
          j++;
        }
      } else {
        result++;
        i++;
        j++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-matching-of-players-with-trainers/submissions/1695951908/){:target="_blank"}

# 설명
1. players의 각 플레이어는 자신의 능력보다 크거나 같은 trainers 내 트레이너를 선택할 수 있으며, 가장 많이 매칭할 수 있는 조합의 수를 반환하는 문제이다.

2. players와 trainers를 오름차순으로 정렬해준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- i와 j는 players와 trainers를 탐색할 위치 변수로, 0으로 초기화한다.
- result는 가장 많이 매칭할 수 있는 조합의 수를 계산할 변수로, 0으로 초기화한다.

4. j가 trainers 이하면서 i가 players 이하일 때 까지 아래를 반복한다.
- players[i] 값이 trainers[j] 값보다 큰 경우, j가 trainers 길이 미만이면서 trainers[j] 값이 players[i] 값보다 작을 때 까지 j를 증가시켜준다.
- players[i] 값이 trainers[j] 값보다 작거나 같은 매칭이 가능한 경우, result와 i, j의 값 모두 증가시켜준다.

5. 반복이 완료되면 매칭된 쌍의 수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumMatchingOfPlayersWithTrainers.java){:target="_blank"}에서 확인 가능합니다.