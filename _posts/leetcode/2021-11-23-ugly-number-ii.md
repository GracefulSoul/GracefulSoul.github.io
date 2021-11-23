---
title: "Leetcode Java Ugly Number II"
excerpt: "Leetcode Ugly Number II Java 풀이"
last_modified_at: 2021-11-23T20:00:00
header:
  image: /assets/images/leetcode/ugly-number-ii.png
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
[Link](https://leetcode.com/problems/ugly-number-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int nthUglyNumber(int n) {
    int[] nums = new int[n];
    nums[0] = 1;
    int index2 = 0;
    int index3 = 0;
    int index5 = 0;
    int factor2 = 2;
    int factor3 = 3;
    int factor5 = 5;
    int min = 1;
    for (int idx = 1; idx < n; idx++) {
      nums[idx] = min = Math.min(Math.min(factor2, factor3), factor5);
      if (min == factor2) {
        factor2 = nums[++index2] * 2;
      }
      if (min == factor3) {
        factor3 = nums[++index3] * 3;
      }
      if (min == factor5) {
        factor5 = nums[++index5] * 5;
      }
    }
    return min;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/591458097/){:target="_blank"}

# 설명
1. 지난 번 [Ugly Number](../ugly-number){:target="_blank"}와 비슷한 문제로, n번째 못생긴 숫자를 반환하는 문제이다.
- 못생긴 숫자는 소인수가 2, 3, 5의 숫자로만 구성된 양의 정수이다.
- 예제를 참고하면, 첫 번째 못생긴 숫자는 1인 것을 알 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums는 n번째 못생긴 숫자를 임시 저장하기 위한 배열로, n의 크기로 정의하고 예제를 참고하여 첫 값에 1을 넣어준다.
- index2, index3, index5는 각 소인수 별 횟수를 저장하는 정수이다.
- factor2, factor3, factor5는 각 소인수의 배수를 저장하는 정수이다.
- min은 n번째 못생긴 숫자를 임시 저장하기 위한 정수이다.

3. 1부터 n 이전까지 반복하여 nums에 못생긴 숫자를 순서대로 넣어준다.

4. nums[idx]와 min에 factor2, factor3, factor5 중 가장 작은 값을 넣어준다.
- 못생긴 숫자인 각 정수들을 순서대로 nums에 넣기 위한 방법이다.

5. min의 값에 따라 아래를 수행한다.
- min이 factor2와 동일한 값이면, index2를 증가시키고 nums의 index2번째 값을 가져와 2를 곱한 값을 factor2에 넣어준다.
- min이 factor3과 동일한 값이면, index3를 증가시키고 nums의 index3번째 값을 가져와 3를 곱한 값을 factor3에 넣어준다.
- min이 factor5와 동일한 값이면, index5를 증가시키고 nums의 index5번째 값을 가져와 5를 곱한 값을 factor5에 넣어준다.
- 위 수행이 개별 검증인 이유는, 공배수인 값의 경우 index와 factor를 공통으로 증가시키기 위함이다.

6. 반복이 완료되면 min의 값 혹은 nums[$n - 1$]의 값을 주어진 문제의 결과로 반환한다.
- 반복은 $n - 1$번까지 반복되므로, min의 값과 nums[$n - 1$]의 값은 동일하다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UglyNumberII.java){:target="_blank"}에서 확인 가능합니다.