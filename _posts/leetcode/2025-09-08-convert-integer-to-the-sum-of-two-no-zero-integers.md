---
title: "Leetcode Java Convert Integer to the Sum of Two No-Zero Integers"
excerpt: "Leetcode - 'Convert Integer to the Sum of Two No-Zero Integers' 문제 Java 풀이"
last_modified_at: 2025-09-08T22:00:00
header:
  image: /assets/images/leetcode/convert-integer-to-the-sum-of-two-no-zero-integers.png
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
[Link](https://leetcode.com/problems/convert-integer-to-the-sum-of-two-no-zero-integers/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] getNoZeroIntegers(int n) {
    int[] result = new int[] { 0, n };
    while (result[0]++ < result[1]--) {
      if (this.isNoZeroInteger(result[0]) && this.isNoZeroInteger(result[1])) {
        break;
      }
    }
    return result;
  }

  private boolean isNoZeroInteger(int num) {
    while (num >= 1) {
      if (num % 10 == 0) {
        return false;
      }
      num /= 10;
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/convert-integer-to-the-sum-of-two-no-zero-integers/submissions/1763635954/){:target="_blank"}

# 설명
1. 0이 포함되지 않은 두 숫자의 합이 n이 되는 두 숫자를 구하는 문제이다.

2. result는 합이 n이 되는 두 숫자를 저장하기 위한 변수로, 0과 n로 구성된 정수 배열로 초기화한다.

3. result[0]의 값이 result[1]의 값보다 작을 때까지 result[0]의 값을 증가시키고, result[1]의 값을 감소시키며 아래를 반복한다.
- result[0]의 값과 result[1]의 값에 0이 포함되는지 여부를 검증하여 둘 다 만족하는 경우, 반복을 종료한다.

4. 계산된 두 숫자가 저장된 배열인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConvertIntegerToTheSumOfTwoNoZeroIntegers.java){:target="_blank"}에서 확인 가능합니다.