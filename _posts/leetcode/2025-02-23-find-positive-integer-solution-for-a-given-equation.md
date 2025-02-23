---
title: "Leetcode Java Find Positive Integer Solution for a Given Equation"
excerpt: "Leetcode - 'Find Positive Integer Solution for a Given Equation' 문제 Java 풀이"
last_modified_at: 2025-02-23T10:50:00
header:
  image: /assets/images/leetcode/find-positive-integer-solution-for-a-given-equation.png
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
[Link](https://leetcode.com/problems/find-positive-integer-solution-for-a-given-equation/){:target="_blank"}

# 코드
```java
/*
 * // This is the custom function interface.
 * // You should not implement it, or speculate about its implementation
 * interface CustomFunction {
 *     // Returns f(x, y) for any given positive integers x and y.
 *     // Note that f(x, y) is increasing with respect to both x and y.
 *     // i.e. f(x, y) < f(x + 1, y), f(x, y) < f(x, y + 1)
 *     public int f(int x, int y);
 * };
 */
class Solution {

  public List<List<Integer>> findSolution(CustomFunction customfunction, int z) {
    List<List<Integer>> result = new ArrayList<>();
    int x = 1;
    int y = 1000;
    while (x <= 1000 && y > 0) {
      int value = customfunction.f(x, y);
      if (value < z) {
        x++;
      } else if (value > z) {
        y--;
      } else {
        result.add(Arrays.asList(x++, y--));
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-positive-integer-solution-for-a-given-equation/submissions/1552251207/){:target="_blank"}

# 설명
1. 숨겨진 함수인 f(x, y)의 결과 값 z를 이용하여 양의 정수 쌍 x와 y을 유추하여 어떠한 순서로든 반환하는 문제이다.
- 정확한 공식은 숨어있지만, 값은 아래와 같이 단조롭게 증가한다.
  - $f(x, y) < f(x + 1, y)$
  - $f(x, y) < f(x, y + 1)$

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 유추된 값들을 저장할 변수로, ArrayList로 초기화한다.
- x와 y는 값의 하한값과 상한값을 저장할 변수로, 1과 1000으로 초기화한다.

3. x가 1000 이하이면서 y가 0 초과일 때 까지 아래를 반복한다.
- value는 customfunction 내 f(x, y) 함수를 수행한 결과를 넣어준다.
- value가 z 미만이면 x를 증가시키고, z 초과이면 y를 감소시켜준다.
- value가 z와 동일한 경우, result에 x와 y를 쌍으로 넣어준 후 x를 증가시키고 y를 감소시켜준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindPositiveIntegerSolutionForAGivenEquation.java){:target="_blank"}에서 확인 가능합니다.