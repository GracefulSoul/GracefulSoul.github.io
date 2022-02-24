---
title: "Leetcode Java Rotate Function"
excerpt: "Leetcode Rotate Function Java 풀이"
last_modified_at: 2022-02-24T20:00:00
header:
  image: /assets/images/leetcode/rotate-function.png
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
[Link](https://leetcode.com/problems/rotate-function/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxRotateFunction(int[] nums) {
    int sum = 0;
    int cal = 0;
    int length = nums.length;
    for (int idx = 0; idx < length; idx++) {
      cal += idx * nums[idx];
      sum += nums[idx];
    }
    int max = cal;
    for (int idx = length - 1; idx >= 1; idx--) {
      cal += sum - (length * nums[idx]);
      max = Math.max(max, cal);
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/648027232/){:target="_blank"}

# 설명
1. 주어진 nums를 이용하여 가장 큰 회전 함수의 값을 찾는 문제이다.
- 회전 함수는, $F(k) = (0 \times nums[0]) + ... + ((n - 1) \times nums[n - 1])$으로 구해진다.
- 단, 숫자의 이동은 시계 방향(우측)으로만 가능하다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 nums의 숫자 합계를 구하기 위한 변수로, 0으로 초기화한다.
- cal은 회전 함수의 값을 구한 값을 저장하기 위한 변수로, 0으로 초기화한다.
- length는 정수 배열 nums의 크기를 담아 저장한다.

3. nums를 처음부터 끝까지 반복하여 값의 위치와 값의 곱을 cal에, 값을 sum에 더해준다.

4. 임시로 최대 값인 max에 초기 회전 함수의 결과인 cal 값을 넣어준다.

5. 값의 위치를 마지막 값부터 두 번째 값까지 idx를 감소시키며 반복을 수행한다.
- sum과 $length \times nums[idx]$의 결과를 뺀 후 cal에 더해준다.
- max에 max와 cal 중 큰 값을 넣어준다.
  - 1번에서 설명한 회전 함수는 예제를 통해 아래의 공식으로 구성된다.
```
F(k) = (0 × nums[length - k]) + (1 × num[length - k + 1]) + ... + ((length - 1) × nums[length - (k + 1)])$
F(k - 1) = (0 × nums[length - k + 1]) + (1 × num[length - k + 2]) + ... + ((length - 1) × nums[length - k])
```
  - 그러므로, 아래의 공식이 성립한다.
```
F(k) - F(k - 1)
= nums[length - k + 1] + nums[length - k + 2] + ... + nums[length - (k + 1)] - ((length - 1) × nums[length - k])
= (nums[length - k] + nums[length - k + 1] + ...) - (length × nums[length - k])
= sum - (length × nums[length - k])
```
  - 즉, $F(k) = F(k - 1) + sum - (length \times nums[length - k])$의 공식이 성립하게 된다.
  - $F(1) = F(0) + sum - (length \times nums[length - 1])$이므로, $length - 1$부터 1까지 감소시키며 가장 큰 회전 함수의 값을 구한다.

6. 반복이 완료되면 가장 큰 회전 함수의 값을 저장한 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RotateFunction.java){:target="_blank"}에서 확인 가능합니다.