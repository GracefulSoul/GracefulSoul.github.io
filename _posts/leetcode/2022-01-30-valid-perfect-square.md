---
title: "Leetcode Java Valid Perfect Square"
excerpt: "Leetcode Valid Perfect Square Java 풀이"
last_modified_at: 2022-01-30T11:00:00
header:
  image: /assets/images/leetcode/valid-perfect-square.png
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
[Link](https://leetcode.com/problems/valid-perfect-square/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isPerfectSquare(int num) {
    int left = 1;
    int right = num;
    while (left <= right) {
      int mid = left + ((right - left) / 2);
      int result = num / mid;
      if (result == mid && num % mid == 0) {
        return true;
      } else if (result < mid) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/630552571/){:target="_blank"}

# 설명
1. 주어진 정수 num이 완전 제곱수인지를 검증하는 문제이다.
- 단, 내장 함수를 사용할 수 없다.

2. 문제 풀이에 필요한 변수를 정의한다.
- left는 제곱수인지 검증하기 위한 제곱근을 가능한 가장 작은 수인 1 부터 찾기 위한 변수로, 1로 초기화 한다.
- right도 제곱수인지 검증하기 위한 제곱근을 가능한 가장 큰 수인 num부터 찾기 위한 변수로, num으로 초기화 한다.

3. left가 right보다 작거나 같을 때까지 반복한다.
- mid에 $left + \frac{right - left}{2}$의 값을 넣어준다.
- result에 $\frac{num}{mid}$를 넣고 아래를 검증한다.
  - result가 mid와 같고 num에 mid를 나눈 나머지 값이 0인 경우 mid의 제곱이 num이 되므로, true를 주어진 문제의 결과로 반환한다.
  - result가 mid보다 작은 경우 예측 가능한 숫자를 작게 좁히기 위해, right에 $mid - 1$을 넣어준다.
  - 그 외의 경우 예측 가능한 숫자를 크게 좁히기 위해, left에 $mid + 1$를 넣어준다.

4. 반복이 완료되면 완전 제곱수가 아니므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidPerfectSquare.java){:target="_blank"}에서 확인 가능합니다.