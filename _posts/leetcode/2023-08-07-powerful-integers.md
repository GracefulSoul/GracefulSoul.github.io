---
title: "Leetcode Java Powerful Integers"
excerpt: "Leetcode Medium - 'Powerful Integers' 문제 Java 풀이"
last_modified_at: 2023-08-07T18:40:00
header:
  image: /assets/images/leetcode/powerful-integers.png
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
[Link](https://leetcode.com/problems/powerful-integers){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> powerfulIntegers(int x, int y, int bound) {
    Set<Integer> result = new HashSet<>();
    for (int i = 1; i < bound; i *= x) {
      for (int j = 1; i + j <= bound; j *= y) {
        result.add(i + j);
        if (y == 1) {
          break;
        }
      }
      if (x == 1) {
        break;
      }
    }
    return new ArrayList<>(result);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/powerful-integers/submissions/1014549929/){:target="_blank"}

# 설명
1. 아래의 조건을 만족하는 [0, bound] 범위 내 숫자들을 반환하는 문제이다.
- i와 j가 0 이상일 때 $x^i + y^j$로 표현 가능해야한다.

2. result는 결과에 해당하는 숫자들을 저장할 변수로, 중복을 제거하기 위해 HashSet으로 초기화한다.

3. 1부터 bound 미만까지 i에 x를 곱하면서 아래를 반복한다.
- 1부터 $i + j$가 bound 이하일 때까지 j에 y를 곱해서 아래를 반복한다.
  - result에 $i + j$를 넣어준다.
  - y가 1인 경우, 증가폭이 없으므로 반복을 그만둔다.
- x가 1인 경우, 위와 동일하게 증가폭이 없으므로 반복을 그만둔다.

4. 반복이 완료되면 result를 ArrayList로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PowerfulIntegers.java){:target="_blank"}에서 확인 가능합니다.