---
title: "Leetcode Java Reveal Cards In Increasing Order"
excerpt: "Leetcode Reveal Cards In Increasing Order Java"
last_modified_at: 2023-07-18T19:20:00
header:
  image: /assets/images/leetcode/reveal-cards-in-increasing-order.png
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
[Link](https://leetcode.com/problems/reveal-cards-in-increasing-order){:target="_blank"}

# 코드
```java
class Solution {

  public int[] deckRevealedIncreasing(int[] deck) {
    int length = deck.length;
    Arrays.sort(deck);
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < length; i++) {
      queue.add(i);
    }
    int[] result = new int[length];
    for (int i = 0; i < length; i++) {
      result[queue.poll()] = deck[i];
      queue.add(queue.poll());
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reveal-cards-in-increasing-order/submissions/997491489/){:target="_blank"}

# 설명
1. 정수 배열인 deck의 값들을 아래의 규칙대로 제거할 수 있는 순서로 값을 정렬하는 문제이다.
- deck의 첫 값을 제거하면 다음 값을 deck의 맨 뒤로 이동시킨다.
- 가장 작은 값을 deck의 맨 앞에 위치시켜 값이 커지는 순으로 마지막 값까지 오름차순으로 제거한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 deck의 길이를 저장한 변수이다.
- queue는 순차적으로 값을 제거하기 위한 순서를 정의하기 위해 필요한 변수로, LinkedList로 초기화하고 deck를 정렬 후 0부터 length까지 순차적으로 queue에 넣어준다.
- result는 결과를 저장할 변수로, length 길이의 정수 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 수행한다.
- result의 queue의 맨 앞 값을 꺼내 해당 위치에 deck의 i번째 값을 넣어준다.
- queue에 queue의 값을 꺼내서 뒤로 넣어준다.

4. 반복이 완료되면 조건에 만족하도록 정렬된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RevealCardsInIncreasingOrder.java){:target="_blank"}에서 확인 가능합니다.