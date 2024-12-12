---
title: "Leetcode Java Take Gifts From the Richest Pile"
excerpt: "Leetcode - 'Take Gifts From the Richest Pile' 문제 Java 풀이"
last_modified_at: 2024-12-12T19:00:00
header:
  image: /assets/images/leetcode/take-gifts-from-the-richest-pile.png
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
[Link](https://leetcode.com/problems/take-gifts-from-the-richest-pile/){:target="_blank"}

# 코드
```java
class Solution {

  public long pickGifts(int[] gifts, int k) {
    Queue<Integer> queue = new PriorityQueue<>((a, b) -> b - a);
    for (int gift : gifts) {
      queue.add(gift);
    }
    while (k-- > 0) {
      queue.add((int) Math.sqrt(queue.poll()));
    }
    long result = 0;
    while (!queue.isEmpty()) {
      result += queue.poll();
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/take-gifts-from-the-richest-pile/submissions/1476888325/){:target="_blank"}

# 설명
1. gifts 내에서 k번 수행마다 가장 큰 값을 제곱근된 값으로 치환 후 남은 선물 갯수의 합을 반환하는 문제이다.

2. queue는 gifts 내 값을 내림차순으로 저장하기 위한 변수로, PriorityQueue로 초기화하고 gifts의 모든 값을 넣어준다.

3. k가 0 초과일 때 까지 아래를 반복하며 k를 감소시킨다.
- queue에 가장 큰 값인 앞의 값을 꺼내 제곱근 계산 후 다시 넣어준다.

4. result에 queue의 모든 값을 더한 후 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TakeGiftsFromTheRichestPile.java){:target="_blank"}에서 확인 가능합니다.