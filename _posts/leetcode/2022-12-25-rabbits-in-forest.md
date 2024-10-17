---
title: "Leetcode Java Rabbits in Forest"
excerpt: "Leetcode - 'Rabbits in Forest' 문제 Java 풀이"
last_modified_at: 2022-12-25T09:50:00
header:
  image: /assets/images/leetcode/rabbits-in-forest.png
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
[Link](https://leetcode.com/problems/rabbits-in-forest){:target="_blank"}

# 코드
```java
class Solution {

  public int numRabbits(int[] answers) {
    int result = 0;
    int[] count = new int[1000];
    for (int answer : answers) {
      if (count[answer] % (answer + 1) == 0) {
        result += answer + 1;
      }
      count[answer]++;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/rabbits-in-forest/submissions/865001680/){:target="_blank"}

# 설명
1. 숲 안에 있는 n마리의 토끼에게 자신과 동일한 색상의 토끼의 수를 물어본 결과가 담긴 answers 배열을 이용하여 숲 안에 있을 최소 토끼의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최소 토끼의 수를 저장하기 위한 변수로, 0으로 초기화한다.
- count는 최소 토끼의 수를 계산하기 위한 배열로, answers의 최대 크기인 1000으로 초기화한다.

3. answers의 각 값을 answer에 넣어 아래를 반복한다.
- count의 answer번째 값에 $answer + 1$을 나눈 나머지가 0인 경우, result에 $answer + 1$을 더해준다.
- count의 answer번째 값을 증가시켜준다.

4. 반복이 완료되면 최소 토끼의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 해설
- count 배열의 answer번째 값에 $answer + 1$의 값을 나눈 경우가 0이면, 아래의 각 경우 별 토끼의 수를 계산할 수 있다.
  - [1, 1]의 경우, 대답한 두 토끼는 각각 자신과 동일한 토끼가 한 마리 더 있다고 대답했으므로 대답한 두 마리의 토끼는 같은 색상인 경우가 될 수 있으므로 최소 토끼의 수는 두 마리이다.
  - [1, 1, 1]의 경우, 첫 번째와 세 번째 대답한 토끼는 위의 조건을 만족하는 경우로 자신과 동일한 토끼가 한 마리 더 있다고 하였으므로 첫 번째와 두 번째가 같은 색상의 토끼로 가정하고 세 번째 토끼는 자신과 같은 색상의 토끼가 있지만 그 토끼는 응답하지 않은 경우가 될 수 있으므로 최소 토끼의 수는 네 마리이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RabbitsInForest.java){:target="_blank"}에서 확인 가능합니다.