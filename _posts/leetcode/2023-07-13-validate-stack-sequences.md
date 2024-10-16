---
title: "Leetcode Java Validate Stack Sequences"
excerpt: "Leetcode Validate Stack Sequences Java"
last_modified_at: 2023-07-13T18:50:00
header:
  image: /assets/images/leetcode/validate-stack-sequences.png
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
[Link](https://leetcode.com/problems/validate-stack-sequences){:target="_blank"}

# 코드
```java
class Solution {

  public boolean validateStackSequences(int[] pushed, int[] popped) {
    Stack<Integer> stack = new Stack<>();
    int i = 0;
    for (int value : pushed) {
      stack.push(value);
      while (!stack.isEmpty() && stack.peek() == popped[i]) {
        stack.pop();
        i++;
      }
    }
    return stack.isEmpty();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/validate-stack-sequences/submissions/993364785/){:target="_blank"}

# 설명
1. 초기화된 스택에서 순차적으로 pushed의 값을 넣고 popped의 값을 꺼낼 수 있는지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- stack은 검증에 필요한 변수로, Stack으로 초기화한다.
- i는 popped의 위치 변수로, 0으로 초기화한다.

3. pushed의 모든 값을 value에 순차적으로 넣고 아래를 수행한다.
- stack에 value를 넣어준다.
- stack이 비어있지 않으면서 stack에서 꺼낸 값이 popped의 i번째 값과 동일할 때까지 반복하여, stack에서 값을 꺼내 제거하고 i를 증가시켜 다음 위치로 이동시킨다.

4. 반복이 완료되면 stack이 비어있는지 검증된 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidateStackSequences.java){:target="_blank"}에서 확인 가능합니다.