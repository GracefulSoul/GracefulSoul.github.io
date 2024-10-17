---
title: "Leetcode Java Divide Players Into Teams of Equal Skill"
excerpt: "Leetcode Medium - 'Divide Players Into Teams of Equal Skill' 문제 Java 풀이"
last_modified_at: 2024-10-04T18:40:00
header:
  image: /assets/images/leetcode/divide-players-into-teams-of-equal-skill.png
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
[Link](https://leetcode.com/problems/divide-players-into-teams-of-equal-skill/){:target="_blank"}

# 코드
```java
class Solution {

  public long dividePlayers(int[] skill) {
    int[] count = new int[1001];
    int sum = 0;
    for (int s : skill) {
      count[s]++;
      sum += s;
    }
    int teams = skill.length / 2;
    if (sum % teams != 0) {
      return -1;
    } else {
      long result = 0;
      int divide = sum / teams;
      for (int s : skill) {
        int diff = divide - s;
        if (count[diff] == 0) {
          return -1;
        }
        result += (long) s * diff;
        count[diff]--;
      }
      return result / 2;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/divide-players-into-teams-of-equal-skill/submissions/1411411923/){:target="_blank"}

# 설명
1. skill을 두 값씩 팀을 지어 동일한 합의 값을 만들 때, 각 팀 값들에 대한 곱을 누계한 값을 반환한다.
- 단, 팀을 이뤄 값을 반환할 수 없으면 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 skill 값의 갯수를 더할 배열로, 값의 범위보다 1 큰 1001 크기의 정수 배열로 초기화하고 갯수를 넣어준다.
- sum은 skill 값의 총합을 넣을 변수로, 각 값의 합을 더해서 넣어준다.
- teams는 skill 값으로 구성할 수 있는 팀의 갯수로, skill 길이를 2로 나눈 값을 넣어준다.

3. sum을 teams로 나눈 값이 0이 아니면 팀을 이룰 수 없으므로, -1을 주어진 문제의 결과로 반환한다.

4. 3번의 경우가 아니라면 아래를 수행한다.
- 결과를 구하기 위한 변수를 정의한다.
  - result는 팀을 이룰 수 있는 값들에 대한 곱을 누계할 변수로, 반환 타입인 long 형태의 0으로 초기화한다.
  - divide는 각 팀이 가능한 값의 합을 저장할 변수로, $\frac{sum}{teams}$로 초기화한다.
- skill을 순차적우로 s에 넣어 아래를 수행한다.
  - diff에 $divide - s$의 팀을 이룰 수 있는 값을 넣어준다.
  - count[diff]가 0인 팀을 이룰 수 없는 경우, -1을 주어진 문제의 결과로 반환한다.
  - result에 s와 diff를 곱한 값을 더한 후 count[diff]의 값을 감소시킨다.
- 반복이 완료되면 각 팀의 값을 두 번 곱해진 result를 2로 나눈 $\frac{result}{2}$를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DividePlayersIntoTeamsOfEqualSkill.java){:target="_blank"}에서 확인 가능합니다.