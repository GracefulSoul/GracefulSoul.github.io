---
title: "Leetcode Java X of a Kind in a Deck of Card"
excerpt: "Leetcode X of a Kind in a Deck of Card Java"
last_modified_at: 2023-05-03T20:50:00
header:
  image: /assets/images/leetcode/x-of-a-kind-in-a-deck-of-cards.png
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
[Link](https://leetcode.com/problems/x-of-a-kind-in-a-deck-of-cards){:target="_blank"}

# 코드
```java
class Solution {

  public boolean hasGroupsSizeX(int[] deck) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int num : deck) {
      map.put(num, map.getOrDefault(num, 0) + 1);
    }
    int result = 0;
    for (int num : map.values()) {
      result = this.getGcd(num, result);
    }
    return result > 1;
  }

  private int getGcd(int m, int n) {
    if (n == 0) {
      return m;
    } else {
      return this.getGcd(n, m % n);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/x-of-a-kind-in-a-deck-of-cards/submissions/943772698/){:target="_blank"}

# 설명
1. 정수 배열인 deak을 이용하여 크기의 같은 값으로 이루어진 동일한 크기의 그룹으로 구성할 수 있는지 검증하는 문제이다.
- 단, 그룹의 크기는 한 개 초과여야 한다.

2. map은 deck의 숫자 별 발생 횟수를 저장할 변수로, key가 deck[i]인 num으로 발생 횟수를 value에 넣어준다.

3. result는 최소 공약수를 저장할 변수로, map의 값들인 발생 횟수를 반복하여 최대 공약수를 넣어 1 초과인지 여부를 주어진 문제의 결과로 반환한다.

# 해설
- deak의 숫자들을 같은 값끼리 동일한 크기 그룹으로 지어야 하는 조건은, 간단히 이야기하면 한 개의 값으로 구성된 그룹은 존재하면 안 된다는 의미이다.
- 또한 두 개 이상의 동일한 값으로 구성해야 한다는 것은 최대 공약수 크기로 분배 가능하면 구성 가능하다고 볼 수 있다.
- [1, 1, 1, 2, 2, 2, 3, 3]을 예를 들어보자.
  - 1과 2는 세 개, 3은 두 개이지만, 두 개 이상의 크기의 그룹을 지어야 하므로 1과 2가 1개씩 남게된다.
  - 이는 3, 3, 2의 최대 공약수가 1이므로 구성이 불가능하다.
- [1, 1, 1, 1, 2, 2, 3, 3]을 예를 들어보자.
  - 1은 네 개, 2와 3은 두 개로, 1로 구성된 두 그룹과 2와 3의 그룹으로 이루어질 수 있다.
  - 이는 4, 2, 2의 최대 공약수가 2이므로 구성이 가능하다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/XOfAKindInADeckOfCards.java){:target="_blank"}에서 확인 가능합니다.