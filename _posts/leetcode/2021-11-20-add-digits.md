---
title: "Leetcode Java Add Digits"
excerpt: "Leetcode Add Digits Java 풀이"
last_modified_at: 2021-11-20T10:00:00
header:
  image: /assets/images/leetcode/add-digits.png
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
[Link](https://leetcode.com/problems/add-digits/){:target="_blank"}

# 코드
```java
class Solution {

  public int addDigits(int num) {
    return ((num - 1) % 9) + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/589779693/){:target="_blank"}

# 설명
1. 주어진 num을 이용하여 각 자릿수를 더한 값으로 결과를 만들어 한 자리가 될 때 까지 수행한 결과를 반환하는 문제이다.
- 단, 반복이나 재귀 호출 없이 O(1)의 시간 복잡도로 만드는 것을 요구한다.

2. 주어진 num에 1을 뺀 값에 9를 나눈 나머지 값의 1을 더한 결과를 주어진 문제의 결과로 반환한다.
- 해당 문제의 결과는 num이 0인 경우를 제외한 모든 숫자에는 1 이상의 숫자가 포함되기 때문에, 각 자리의 합을 통해 한 자리의 숫자를 만들게 되면 1 ~ 9 까지의 결과만 존재한다.
- num의 자리에 $num - 1$, 9로 나눈 나머지의 값에 1을 더하는 보정치를 적용하여 결과를 적용한다.
- 아래의 예를 보자.
  - 주어진 num이 99인 경우, $9 + 9 = 18$, $1 + 8 = 9$로 결과는 9가 나온다.
  - 단순히 9로 나누는 경우, $99 % 9 = 0$으로 원하는 결과가 나오지 않는다.
  - 위의 보정을 통해 $((99 - 1) % 9) + 1 = 9$로 값을 빼서 나눈 결과에 1을 더해주면 제시된 결과와 동일한 결과가 나온다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/AddDigits.java){:target="_blank"}에서 확인 가능합니다.