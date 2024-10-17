---
title: "Leetcode Java Baseball Game"
excerpt: "Leetcode - 'Baseball Game' 문제 Java 풀이"
last_modified_at: 2022-10-04T08:10:00
header:
  image: /assets/images/leetcode/baseball-game.png
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
[Link](https://leetcode.com/problems/baseball-game){:target="_blank"}

# 코드
```java
class Solution {

  public int calPoints(String[] operations) {
    Stack<Integer> stack = new Stack<>();
    int sum = 0;
    for (String operation : operations) {
      int num;
      switch (operation) {
        case "+":
          num = stack.pop();
          int add = num + stack.peek();
          sum += add;
          stack.push(num);
          stack.push(add);
          break;
        case "D":
          num = stack.peek() * 2;
          sum += num;
          stack.push(num);
          break;
        case "C":
          sum -= stack.pop();
          break;
        default:
          num = Integer.parseInt(operation);
          sum += num;
          stack.push(num);
      }
    }
    return sum;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/814952148/){:target="_blank"}

# 설명
1. operations의 모든 값들을 순차적으로 아래의 문자에 해당하는 규칙으로 점수를 계산하여 반환하는 문제이다.
- 정수인 경우, 해당 값으로 점수를 기록한다.
- "+" 문자인 경우, 이전 두 정수인 점수들의 합으로 점수를 기록한다.
- "D" 문자인 경우, 이전 정수인 점수의 두 배로 점수를 기록한다.
- "C" 문자인 경우, 이전 정수인 점수를 무효 처리하여 제거한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- stack은 기록된 점수를 순차적으로 넣고 꺼내 계산하기 위한 변수로, Stack으로 초기화한다.
- sum은 계산된 최종 점수를 저장할 변수로, 0으로 초기화한다.

3. oprations의 모든 문자열을 operation로 아래를 반복한다.
- num은 stack에서 꺼내 임시 보관할 변수이다.
- operation이 "+" 문자인 경우 아래를 수행한다.
  - num에 stack에서 값을 꺼내 넣어주고, add에 num과 stack의 다음 값을 더해준다.
  - sum에 add를 더해 두 점수의 합을 더해준다.
  - stack에 num과 add를 순서대로 다시 넣어 다음 계산에 포함되도록 한다.
- operation이 "D" 문자인 경우 아래를 수행한다.
  - num에 stack의 이전 값의 두 배를 넣어준다.
  - sum에 num을 더해주고, stack에 현재 점수인 num을 넣어준다.
- operation이 "C" 문자인 경우 아래를 수행한다.
  - sum에 stack의 값을 꺼내 빼준다.
- 위의 문자들이 아닌 경우 숫자이므로 아래를 수행한다.
  - num에 operation을 숫자로 변환해 넣어준다.
  - sum에 num을 더하고, stack에 num을 넣어준다.

4. 반복이 완료되면 계산된 총점인 sum을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BaseballGame.java){:target="_blank"}에서 확인 가능합니다.