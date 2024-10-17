---
title: "Leetcode Java Bag of Tokens"
excerpt: "Leetcode Medium - 'Bag of Tokens' 문제 Java 풀이"
last_modified_at: 2023-07-17T19:10:00
header:
  image: /assets/images/leetcode/bag-of-tokens.png
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
[Link](https://leetcode.com/problems/bag-of-tokens){:target="_blank"}

# 코드
```java
class Solution {

  public int bagOfTokensScore(int[] tokens, int power) {
    Arrays.sort(tokens);
    int result = 0;
    int points = 0;
    int left = 0;
    int right = tokens.length - 1;
    while (left <= right) {
      if (tokens[left] <= power) {
        power -= tokens[left++];
        result = Math.max(result, ++points);
      } else if (points > 0) {
        points--;
        power += tokens[right--];
      } else {
        break;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/bag-of-tokens/submissions/996562855/){:target="_blank"}

# 설명
1. 아래의 두 방법을 이용하여 얻을 수 있는 최대 점수를 반환하는 문제이다.
- 현재 power가 i번째 토큰 이상이면, 해당 토큰의 값을 power에서 빼고 1점을 얻게된다.
- 현재 점수가 1점 이상이면, 토큰의 값을 power에 저장하고 1점을 잃게된다.
- 토큰은 임의의 순서대로 수행할 수 있으며, 모든 토큰을 수행할 필요는 없다.

2. tokens의 값을 오름차순으로 정렬한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장할 변수로, 0으로 초기화한다.
- points는 포인트를 계산할 변수로, 0으로 초기화한다.
- left와 right는 좌측과 우측의 위치를 저장할 변수로, 0과 tokens의 길이보다 1 작은 값으로 초기화한다.

4. left가 right 미만일 때 까지 아래를 반복한다.
- tokens의 left번째 값이 power보다 작거나 같은 경우, 아래를 수행한다.
  - power에 tokens의 left번째 값을 빼고 left를 감소시킨다.
  - points를 증가시키고 result에 result와 points 중 큰 값을 넣어준다.
- 위의 경우가 아니면서 points의 값이 0보다 큰 경우, 아래를 수행한다.
  - points의 값을 감소시키고, power에 tokens의 right번째 값을 더해주고 right를 감소시킨다.
- 위의 모든 경우가 아니라면 반복을 중지하여 계산을 그만둔다.

5. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BagOfTokens.java){:target="_blank"}에서 확인 가능합니다.