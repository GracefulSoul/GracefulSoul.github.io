---
title: "Leetcode Java Water and Jug Problem"
excerpt: "Leetcode Water and Jug Problem Java 풀이"
last_modified_at: 2022-01-28T13:00:00
header:
  image: /assets/images/leetcode/water-and-jug-problem.png
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
[Link](https://leetcode.com/problems/water-and-jug-problem/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canMeasureWater(int jug1Capacity, int jug2Capacity, int targetCapacity) {
    if (jug1Capacity + jug2Capacity < targetCapacity) {
      return false;
    } else if (jug1Capacity == targetCapacity
        || jug2Capacity == targetCapacity
        || jug1Capacity + jug2Capacity == targetCapacity) {
      return true;
    } else {
      return targetCapacity % this.getGcd(jug1Capacity, jug2Capacity) == 0;
    }
  }

  private int getGcd(int num1, int num2) {
    if (num1 % num2 == 0) {
      return num2;
    } else {
      return this.getGcd(num2, num1 % num2);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/629922027/){:target="_blank"}

# 설명
1. 주어진 정수 jug1Capacity와 jug2Capacity의 용기를 이용하여 정확한 targetCapacity 용량을 측정할 수 있는지를 검증하는 문제이다.

2. jug1Capacity와 jug2Capacity의 합이 targetCapacity보다 작은 경우 두 용기에 물을 채워도 targetCapacity만큼 채울 수 없으므로, 주어진 문제의 결과로 false를 반환한다.

3. jug1Capacity 혹은 jug2Capacity, 두 합이 targetCapacity과 같은 경우는 단번에 targetCapacity만큼 채울 수 있으므로, 주어진 문제의 결과로 true를 반환한다.

4. targetCapacity과 5번에서 정의한 getGcd(jug1Capacity, jug2Capacity) 메서드의 나눈 나머지 값이 0인지 여부를 주어진 문제의 결과로 반환한다.

5. 유클리드 호제법[^Euclidean]을 이용한 getGcd(jug1Capacity, jug2Capacity) 메서드를 정의한다.
- num1과 num2의 나눈 나머지 값이 0인 경우, num2를 반환한다.
- 그렇지 않은 경우, num2와 num1과 num2의 나눈 나머지 값을 재귀 호출을 수행한 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WaterAndJugProblem.java){:target="_blank"}에서 확인 가능합니다.

# Reference
[^Euclidean]: [Wiki-Euclidean_Algorithm](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%81%B4%EB%A6%AC%EB%93%9C_%ED%98%B8%EC%A0%9C%EB%B2%95){:target="_blank"}