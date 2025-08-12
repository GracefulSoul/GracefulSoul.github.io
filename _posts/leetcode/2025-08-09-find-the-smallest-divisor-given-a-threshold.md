---
title: "Leetcode Java Find the Smallest Divisor Given a Threshold"
excerpt: "Leetcode - 'Find the Smallest Divisor Given a Threshold' 문제 Java 풀이"
last_modified_at: 2025-08-09T13:30:00
header:
  image: /assets/images/leetcode/find-the-smallest-divisor-given-a-threshold.png
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
[Link](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/){:target="_blank"}

# 코드
```java
class Solution {

  public int smallestDivisor(int[] nums, int threshold) {
    int left = 1;
    int right = (int) 1e6;
    while (left < right) {
      int mid = (left + right) / 2;
      int sum = 0;
      for (int num : nums) {
        sum += (num + mid - 1) / mid;
      }
      if (sum > threshold) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return left;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-smallest-divisor-given-a-threshold/submissions/1728505932/){:target="_blank"}

# 설명
1. 아래 수행을 통해서 모든 배열의 값을 threshold보다 작거나 같도록 할 수 있는 가장 작은 약수를 구하는 문제이다.
- 양의 정수 약수를 선택하여 모든 배열의 값을 이 숫자로 나눈 후 다음 나눗셈 연산에 합산한다.
- 각 나눗셈의 결과는 해당 값보다 크거나 가까운 숫자로 반올림된다.

2. left와 right는 값을 탐색하기 위한 값의 범위로, 값의 하한값인 1과 상한값인 $10^6$으로 각각 초기화한다.

3. left가 right보다 작을 때 까지 아래를 반복한다.
- mid에 $\frac{left + right}{2}$인 중앙값을 넣어준다.
- sum은 합계를 저장할 변수로 0으로 초기화한다.

4. nums의 모든 값을 순차적으로 num에 넣으며 sum에 $\frac{num + mid - 1}{mid}$ 값을 더해준다.

5. sum이 threshold보다 크면 left에 $mid + 1$을, 아니면 right에 mid를 넣어 범위를 축소시킨다.

6. 반복이 완료되면 가능한 가장 작은 약수인 left를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheSmallestDivisorGivenAThreshold.java){:target="_blank"}에서 확인 가능합니다.