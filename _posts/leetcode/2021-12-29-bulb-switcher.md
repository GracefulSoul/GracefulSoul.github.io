---
title: "Leetcode Java Bulb Switcher"
excerpt: "Leetcode Bulb Switcher Java 풀이"
last_modified_at: 2021-12-29T15:00:00
header:
  image: /assets/images/leetcode/bulb-switcher.png
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
[Link](https://leetcode.com/problems/bulb-switcher/){:target="_blank"}

# 코드
```java
class Solution {

  public int bulbSwitch(int n) {
    return (int) Math.sqrt(n);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/609002764/){:target="_blank"}

# 설명
1. 주어진 정수 n개의 전구를 이용하여 아래의 룰대로 수행하여 켜진 전구의 수를 반환하는 문제이다.
- 처음 n개의 전구는 모두 꺼져있다.
- n 번의 라운드를 수행하며, 매 라운드마다 n 번째의 전구를 스위칭하여 꺼진 전구는 켜고, 켜져있는 전구는 꺼준다.

2. 주어진 n의 제곱근을 구하여 정수형으로 형변환한 값을 주어진 문제의 결과로 반환한다.
- n보다 크지 않은 완전 제곱근의 수는 n의 제곱근의 정수부분이므로, Math.sqrt(n)의 결과를 정수형인 int로 형변환하여 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BulbSwitcher.java){:target="_blank"}에서 확인 가능합니다.