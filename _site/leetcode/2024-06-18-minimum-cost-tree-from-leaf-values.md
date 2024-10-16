---
title: "Leetcode Java Minimum Cost Tree From Leaf Values"
excerpt: "Leetcode Minimum Cost Tree From Leaf Values Java"
last_modified_at: 2024-06-18T17:30:00
header:
  image: /assets/images/leetcode/minimum-cost-tree-from-leaf-values.png
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
[Link](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/){:target="_blank"}

# 코드
```java
class Solution {

  public int mctFromLeafValues(int[] arr) {
    int result = 0;
    Stack<Integer> stack = new Stack<>();
    stack.push(Integer.MAX_VALUE);
    for (int num : arr) {
      while (stack.peek() <= num) {
        result += stack.pop() * Math.min(stack.peek(), num);
      }
      stack.push(num);
    }
    while (stack.size() > 2) {
      result += stack.pop() * stack.peek();
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-cost-tree-from-leaf-values/submissions/1292188988/){:target="_blank"}

# 설명
1. arr은 리프 노드로 이루어진 값들로, 가장 작은 부모 노드들 값의 합을 구하는 문제이다.
- 부모 노드의 값은 아래 위치한 리프 노드들 중 가장 큰 값을 가진 두 노드 값의 곱으로 결정된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 부모 노드들 값의 합을 저장할 변수로, 0으로 초기화한다.
- stack은 자식 노드들을 순회하여 부모 노드의 값을 설정하기 위한 변수로, 선입선출의 Stack으로 초기화하고 값의 구분을 위해 첫 값을 정수의 가장 큰 값으로 넣어준다.

3. arr의 각 값을 순차적으로 num에 넣고 아래를 수행한다.
- stack 내 맨 앞의 값이 num보다 작거나 같은 부모 노드 생성이 가능한 값까지 result에 stack의 앞의 값을 꺼내 해당 값과 stack의 현재 맨 앞의 값과 num 중 작은 값을 곱해서 더해준다.
- stack에 num을 넣어준다.

4. 3번이 완료되고 stack의 크기가 2 초과인 잔여 값이 존재하는 경우, 마지막으로 root 노드의 값인 해당 두 값을 곱하여 result에 더해준다.

5. 반복이 완료되면 가장 작은 부모 노드들 값의 합이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ShortestPathWithAlternatingColors.java){:target="_blank"}에서 확인 가능합니다.