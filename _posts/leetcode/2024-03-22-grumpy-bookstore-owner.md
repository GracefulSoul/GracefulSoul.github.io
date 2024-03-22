---
title: "Leetcode Java Grumpy Bookstore Owner"
excerpt: "Leetcode Grumpy Bookstore Owner Java"
last_modified_at: 2024-03-22T19:10:00
header:
  image: /assets/images/leetcode/grumpy-bookstore-owner.png
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
[Link](https://leetcode.com/problems/grumpy-bookstore-owner/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxSatisfied(int[] customers, int[] grumpy, int minutes) {
    int max = 0;
    int sum = 0;
    int[] total = new int[2];
    for (int i = 0; i < customers.length; i++) {
      total[0] += customers[i];
      total[1] += customers[i] * grumpy[i];
      sum += customers[i] * grumpy[i];
      if (i > minutes - 1) {
        sum -= customers[i - minutes] * grumpy[i - minutes];
      }
      max = Math.max(sum, max);
    }
    return total[0] - total[1] + max;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/grumpy-bookstore-owner/submissions/1210779997/){:target="_blank"}

# 설명
1. customers와 grumpy를 이용하여 아래의 규칙에 따라 하루 종일 만족할 수 있는 최대 고객 수를 반환하는 문제이다.
- i분에 customers[i]명의 고객이 방문하고, grumpy[i]의 값은 만족도를 나타낸다.
- grumpy[i]의 값이 1이면 심술을, 만족하면 0을 뜻한다.
- 주인은 minutes분 동안 1회 심술을 방지할 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 minutes분 동안 심술을 방지하고 만족한 최대 고객 수를 저장하기 위한 변수로, 0으로 초기화한다.
- sum은 minutes분 동안 심술을 방지하고 만족한 최대 고객 수를 계산하기 위한 변수로, 0으로 초기화한다.
- total은 방문한 고객의 수와 만족한 고객의 합계를 저장할 변수로, 2차원 정수 배열로 초기화한다.

3. 0부터 customers의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- total[0]에 customers[i]인 고객의 수를 더해준다.
- total[1]에 $customers[i] \times grumpy[i]$인 만족한 고객의 수를 더해준다.
- sum에 $customers[i] * grumpy[i]$를 더해 만족한 고객의 수를 누계한다.
- i가 $minutes - 1$보다 큰 경우, sum에서 $i - minuets$번째 만족한 고객의 수를 빼준다.
- sum에 max와 sum 중 큰 값을 넣어준다.

4. 반복이 완료되면 $total[0] - total[1]$인 만족하지 않은 고객의 수에 minutes 동안 심술을 방지한 최대 고객의 수인 max를 더해 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GrumpyBookstoreOwner.java){:target="_blank"}에서 확인 가능합니다.