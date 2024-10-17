---
title: "Leetcode Java Find the Highest Altitude"
excerpt: "Leetcode Easy - 'Find the Highest Altitude' 문제 Java 풀이"
last_modified_at: 2023-06-19T19:00:00
header:
  image: /assets/images/leetcode/find-the-highest-altitude.png
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
[Link](https://leetcode.com/problems/find-the-highest-altitude){:target="_blank"}

# 코드
```java
class Solution {

  public int largestAltitude(int[] gain) {
    int max = 0;
    int sum = 0;
    for (int num : gain) {
      sum += num;
      if (sum > max) {
        max = sum;
      }
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-highest-altitude/submissions/974649847/){:target="_blank"}

# 설명
1. 고도가 0인 위치에서 순차적으로 고도의 낙폭이 들어있는 gain을 이용하여 가장 높은 고도를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max은 최대 고도를 저장할 변수로, 0으로 초기화한다.
- sum은 고도 변화를 누계할 변수로, 0으로 초기화한다.

3. gain의 모든 값을 num에 순차적으로 넣고 아래를 수행한다.
- sum에 num을 넣고, sum이 max보다 큰 경우 max에 sum을 넣어준다.

4. 반복이 완료되면 최고 고도인 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheHighestAltitude.java){:target="_blank"}에서 확인 가능합니다.