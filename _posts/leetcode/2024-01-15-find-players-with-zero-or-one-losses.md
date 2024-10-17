---
title: "Leetcode Java Find Players With Zero or One Losses"
excerpt: "Leetcode Medium - 'Find Players With Zero or One Losses' 문제 Java 풀이"
last_modified_at: 2024-01-15T18:50:00
header:
  image: /assets/images/leetcode/find-players-with-zero-or-one-losses.png
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
[Link](https://leetcode.com/problems/find-players-with-zero-or-one-losses){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> findWinners(int[][] matches) {
    int[] count = new int[100001];
    for (int i = 0; i < matches.length; i++) {
      int win = matches[i][0];
      int lose = matches[i][1];
      if (count[win] == 0) {
        count[win] = -1;
      }
      if (count[lose] == -1) {
        count[lose] = 1;
      } else {
        count[lose]++;
      }
    }
    List<List<Integer>> result = Arrays.asList(new ArrayList<>(), new ArrayList<>());
    for (int i = 0; i < count.length; i++) {
      if (count[i] == -1) {
        result.get(0).add(i);
      } else if (count[i] == 1) {
        result.get(1).add(i);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-players-with-zero-or-one-losses/submissions/1146766054/){:target="_blank"}

# 설명
1. 아래와 같은 값이 있는 matches를 이용하여 한 번도 패배하지 않은 사람과 한 번만 패배한 사람을 모아 반환하는 문제이다.
- matches[i] = [winner<sub>i</sub>, loser<sub>i</sub>]를 나타낸다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 패배 횟수를 저장할 변수로, 0부터 matches의 길이 미만까지 i를 증가시키며 아래의 규칙대로 값을 넣어준다.
  - win에는 matches[i][0]인 승리한 사람의 번호를, lose에는 matches[i][1] 패배한 사람의 번호를 넣어준다.
  - count[win]이 0인 패배한적이 없는 사람인 경우, -1을 넣어 패배하지 않았다는 것을 표시해준다.
  - count[lose]의 값이 -1이면 1로, 그 외는 값을 증가시켜준다.
- result는 결과 값을 넣기 위한 변수로, ArrayList에 패배하지 않은 사람이 들어갈 ArrayList와 한 번만 패배한 사람이 들어갈 ArrayList를 넣어 초기화한다.

3. 0부터 count의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- count[i]가 -1이면 패배한 적이 없으므로, result의 첫번째 ArrayList에 해당 사람의 번호인 i를 넣어준다.
- count[i]가 1이면 한 번만 패배하였으므로, result의 두번째 ArrayList에 해당 사람의 번호인 i를 넣어준다.

4. 반복이 완료되면 각 그룹이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindPlayersWithZeroOrOneLosses.java){:target="_blank"}에서 확인 가능합니다.