---
title: "Leetcode Java Minimum Operations to Make the Integer Zero"
excerpt: "Leetcode - 'Minimum Operations to Make the Integer Zero' 문제 Java 풀이"
last_modified_at: 2025-09-05T19:00:00
header:
  image: /assets/images/leetcode/minimum-operations-to-make-the-integer-zero.png
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
[Link](https://leetcode.com/problems/minimum-operations-to-make-the-integer-zero/){:target="_blank"}

# 코드
```java
class Solution {

  public int makeTheIntegerZero(int num1, int num2) {
    for (int i = 1; i <= 60; i++) {
      long num = num1 - ((long) num2 * i);
      if (num < i) {
        return -1;
      }
      if (Long.bitCount(num) <= i) {
        return i;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-operations-to-make-the-integer-zero/submissions/1760303077/){:target="_blank"}

# 설명
1. num1과 num2가 주어지면 [0, 60] 범위의 i를 이용해서 $2^i + num2$의 값을 num1에서 뺄 때 0을 만들기 위한 최소 횟수를 계산하는 문제이다.
- 단, 0을 만들 수 없다면 -1을 주어진 문제의 결과로 반환한다.

2. 1부터 60 이하까지 i를 증가시키며 아래를 반복한다.
- num은 i에 대해서 조건을 수행한 결과를 저장한 변수로, $num1 - (num2 \times i)$의 값으로 초기화한다.
  - $2^i + num2$의 값을 i가 1부터 현재 위치까지 누계하는 경우, $num1 - (2^1 + 2^2 + ... + 2^i) + (num2 \times i)$이 된다.
  - $num1 - (2^1 + 2^2 + ... + 2^i) + (num2 \times i) = 0$이 만족해야 조건을 충족하므로, $(2^1 + 2^2 + ... + 2^i) = num1 - (num2 \times i)$를 만족한다.
  - 위를 통해서 현재 위치인 i에서 num을 $num1 - (num2 \times i)$의 값으로 설정한다.
- num이 i보다 작은 0을 만들 수 없는 경우, -1을 주어진 문제의 결과로 반환한다.
- num의 비트 중 1의 갯수가 i보다 작은 i번의 수행을 통해 0을 만들 수 있는 경우, i를 주어진 문제의 결과로 반환한다.

3. 반복이 완료되면 주어진 조건을 통해 0을 만들 수 없으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumOperationsToMakeTheIntegerZero.java){:target="_blank"}에서 확인 가능합니다.