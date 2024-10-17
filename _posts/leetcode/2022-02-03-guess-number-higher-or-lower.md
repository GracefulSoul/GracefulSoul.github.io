---
title: "Leetcode Java Guess Number Higher or Lower"
excerpt: "Leetcode - 'Guess Number Higher or Lower' 문제 Java 풀이"
last_modified_at: 2022-02-03T13:00:00
header:
  image: /assets/images/leetcode/guess-number-higher-or-lower.png
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
[Link](https://leetcode.com/problems/guess-number-higher-or-lower/){:target="_blank"}

# 코드
```java
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return        -1 if num is lower than the guess number
 *            1 if num is higher than the guess number
 *               otherwise return 0
 * int guess(int num);
 */

public class Solution extends GuessGame {

  public int guessNumber(int n) {
    int low = 1;
    int high = n;
    while (low < high) {
      int mid = low + ((high - low) / 2);
      switch (super.guess(mid)) {
        case -1: high = mid; break;
        case 1: low = mid + 1; break;
        case 0: return mid;
      }
    }
    return low;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/633388641/){:target="_blank"}

# 설명
1. GuessGame의 guess(int num) 메서드 호출 결과로 1과 주어진 정수 n 사이의 임의 숫자 pick을 유추하는 문제이다.
- guess 메서드 호출 결과가 -1인 경우, num > pick 이다.
- guess 메서드 호출 결과가 1인 경우, num < pick 이다.
- guess 메서드 호출 결과가 0인 경우, num == pick 이다.

2. 주어진 문제 풀이에 필요한 변수를 정의한다.
- low는 가능한 가장 작은 수인 1로 초기화한다.
- high는 가능한 가장 큰 수인 n으로 초기화한다.

3. low가 high보다 작을 때 까지 반복한다.
- mid에 $low + \frac{high - low}{2}$의 결과를 넣고, mid를 이용하여 guess 메서드를 호출한다.
  - guess 메서드 호출 결과가 -1인 경우, high에 mid 값을 넣어준다.
  - guess 메서드 호출 결과가 1인 경우, low에 $mid + 1$ 값을 넣어준다.
  - guess 메서드 호출 결과가 0인 경우, mid를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 low를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GuessNumberHigherOrLower.java){:target="_blank"}에서 확인 가능합니다.