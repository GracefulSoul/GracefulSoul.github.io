---
title: "Leetcode Java Water Bottles"
excerpt: "Leetcode Easy - 'Water Bottles' 문제 Java 풀이"
last_modified_at: 2024-07-07T23:20:00
header:
  image: /assets/images/leetcode/water-bottles.png
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
[Link](https://leetcode.com/problems/water-bottles/){:target="_blank"}

# 코드
```java
class Solution {

  public int numWaterBottles(int numBottles, int numExchange) {
    int result = numBottles;
    while (numBottles >= numExchange) {
      int newBottles = numBottles / numExchange;
      result += newBottles;
      numBottles = (numBottles % numExchange) + newBottles;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/water-bottles/submissions/1312930745/){:target="_blank"}

# 설명
1. numBottles 개의 물을 다 마신 후 numExchange 개의 빈 병을 하나의 새 물로 교환해줄 때, 마실 수 있는 물의 갯수를 구하는 문제이다.

2. result는 마실 수 있는 물의 갯수를 저장할 변수로, 처음 주어진 물인 numBottles 개의 물은 모두 마실수 있어 해당 갯수로 초기화한다.

3. numBottles가 numExchange보다 크거나 같을 때 까지 아래를 반복한다.
- newBottles는 빈 병을 numExchange 개 단위로 교환한 새 물의 수를 나타내는 변수로, 최대 교환 가능한 $\frac{numBottles}{numExchange}$의 몫에 대한 갯수를 넣어준다.
- result에 교환한 새 물을 모두 마시는 경우인 newBottles을 더해준다.
- numBottles에 교환하고 남은 $\frac{numBottles}{numExchange}$의 나머지에 대한 갯수에 위에서 교환하여 다 마신 newBottles 개의 공병을 더해준다.

4. 결과가 완료되면 물을 마신 병의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WaterBottles.java){:target="_blank"}에서 확인 가능합니다.