---
title: "Leetcode Java Prime Subtraction Operation"
excerpt: "Leetcode - 'Prime Subtraction Operation' 문제 Java 풀이"
last_modified_at: 2024-11-11T20:00:00
header:
  image: /assets/images/leetcode/prime-subtraction-operation.png
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
[Link](https://leetcode.com/problems/prime-subtraction-operation/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean primeSubOperation(int[] nums) {
    for (int i = 0; i < nums.length; i++) {
      int num;
      if (i == 0) {
        num = nums[0];
      } else {
        num = nums[i] - nums[i - 1];
        if (num <= 0) {
          return false;
        }
      }
      int max = 0;
      for (int j = num - 1; j >= 2; j--) {
        if (this.isPrime(j)) {
          max = j;
          break;
        }
      }
      nums[i] -= max;
    }
    return true;
  }

  private boolean isPrime(int num) {
    for (int i = 2; i <= Math.sqrt(num); i++) {
      if (num % i == 0) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/prime-subtraction-operation/submissions/1449463009/){:target="_blank"}

# 설명
1. nums의 각 위치의 값보다 작은 소수를 현재 값에서 빼서 점층적으로 증가하는 배열을 만들 수 있는지 검증하는 문제이다.

2. 0부터 nums의 길이 미만까지 아래를 반복한다.
- num에 아래의 조건에 해당하는 값을 할당한다.
  - i가 0인 첫 수행인 경우, nums[0]을 넣어준다.
  - 위의 경우가 아니라면 nums[i] - nums[$i - 1$]의 값을 넣은 후, 해당 값이 0 이하인 점층적으로 증가하는 배열을 만들 수 없는 경우 false를 주어진 문제의 결과로 반환한다.
- max는 가능한 소수값을 저장하기 위한 변수로, $num - 1$부터 2 이상까지 j를 감소시키면서 소수인 값을 찾아 넣어준다.
- nums[i]에 max를 빼서 감소된 값을 저장한다.

3. 반복이 완료되면 점층적으로 증가하는 배열을 만들 수 있으므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PrimeSubtractionOperation.java){:target="_blank"}에서 확인 가능합니다.