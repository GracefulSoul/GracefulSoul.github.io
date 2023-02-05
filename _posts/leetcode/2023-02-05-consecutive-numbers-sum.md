---
title: "Leetcode Java Consecutive Numbers Sum"
excerpt: "Leetcode Consecutive Numbers Sum Java"
last_modified_at: 2023-02-05T14:50:00
header:
  image: /assets/images/leetcode/consecutive-numbers-sum.png
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
[Link](https://leetcode.com/problems/consecutive-numbers-sum){:target="_blank"}

# 코드
```java
class Solution {

  public int consecutiveNumbersSum(int n) {
    int result = 1;
    while (n % 2 == 0) {
      n /= 2;
    }
    for (int idx = 3; idx * idx <= n; idx += 2) {
      int count = 1;
      while (n % idx == 0) {
        n /= idx;
        count++;
      }
      result *= count;
    }
    return n == 1 ? result : result * 2;
  }


}
```

# 결과
[Link](https://leetcode.com/problems/consecutive-numbers-sum/submissions/891836138/){:target="_blank"}

# 설명
1. 연속된 숫자의 합으로 n을 만들 수 있는 경우의 수를 구하는 문제이다.

2. reulst는 결과를 저장할 변수로, 자기 자신의 갯수를 포함한 1로 초기화한다.

3. n을 2로 나눈 나머지가 없을 때까지 나누어 상한선을 정의한다.

4. 3부터 idx의 제곱이 n보다 작을 때 까지 2씩 증가하면서 아래를 반복한다.
- count는 갯수를 산정할 변수로, 1로 초기화한다.
- n을 idx로 나눈 나머지가 0일 때 까지 n을 idx로 나누고 count를 증가시킨다.
- result에 count를 곱해준다.

5. n이 1이면 result를, 아니면 result의 2배를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConsecutiveNumbersSum.java){:target="_blank"}에서 확인 가능합니다.