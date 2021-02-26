---
title: "Codility StoneWall"
excerpt: "Lesson7. Stack and Queues"
last_modified_at: 2021-02-21T14:28:00
header:
  image: /assets/images/codility/StoneWall.png
categories:
  - Codility
tags:
  - Programming
  - Codility
  - Stack and Queues

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://app.codility.com/programmers/lessons/7-stacks_and_queues/stone_wall/)

# 코드
```java
// you can also use imports, for example:
// import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

import java.util.Stack;

class Solution {
  public int solution(int[] H) {
    int result = 0;
    Stack<Integer> stack = new Stack<>();
    for (int height : H) {
      while (!stack.isEmpty() && stack.peek() > height) {
        stack.pop(); // Remove higher than new stone wall.
      }
      if (stack.isEmpty() || stack.peek() < height) {
        stack.push(height); // Add new stone wall.
        result++;
      }
    }
    return result;
  }
}
```

# 설명
1. 돌담의 높이를 임시 저장하기 위한 저장소로 Stack을 사용한다.
2. 주어진 배열 H를 반복하여 블록의 수를 계산한다.
    - 돌담의 높이를 임시 저장한 stack이 비어있지 않을 떄, stack에서 꺼낸 돌담의 높이가 주어진 돌담의 높이보다 큰 값들을 제거한다.
        * 주어진 돌담의 높이가 stack에서 꺼낸 돌담의 높이보다 높은 경우는 기존 블록에 새로운 블록을 추가하여 사용하므로 패스한다.
        * 주어진 돌담의 높이가 stack에서 꺼낸 돌담의 높이와 같은 경우는 같은 블록을 사용하므로 무시한다.
        * 주어진 돌담의 높이가 stack에서 꺼낸 돌담의 높이보다 낮은 경우는 새로운 블록을 사용해야 하므로 기존 값을 지운다.
    - stack이 비어있거나 stack에서 꺼낸 돌담의 높이가 주어진 돌담의 높이보다 작으면 새로운 블록을 추가해야 하므로 stack에 추가하고, 블록의 수를 저장하는 result를 증가시킨다.
5. 반복이 완료되면 블록의 수를 저장하는 result를 주어진 문제의 결과로 반환한다.

# 결과
[Link](https://app.codility.com/demo/results/trainingJSWNH2-6PS/)

# 소스
[GitHub-StoneWall](https://github.com/GracefulSoul/Sample/blob/master/src/main/java/gracefulsoul/codility/lesson07/StoneWall.java)