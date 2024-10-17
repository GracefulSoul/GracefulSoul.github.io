---
title: "Leetcode Java Sort Array By Parity II"
excerpt: "Leetcode - 'Sort Array By Parity II' 문제 Java 풀이"
last_modified_at: 2023-05-10T19:25:00
header:
  image: /assets/images/leetcode/sort-array-by-parity-ii.png
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
[Link](https://leetcode.com/problems/sort-array-by-parity-ii){:target="_blank"}

# 코드
```java
class Solution {

  public int[] sortArrayByParityII(int[] nums) {
    int even = 0;
    int odd = 1;
    while (even < nums.length && odd < nums.length) {
      if (nums[even] % 2 == 0) {
        even += 2;
      } else {
        int temp = nums[even];
        nums[even] = nums[odd];
        nums[odd] = temp;
        odd += 2;
      }
    }
    return nums;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sort-array-by-parity-ii/submissions/947775184/){:target="_blank"}

# 설명
1. 지난 번 [Sort Array By Parity](../sort-array-by-parity){:target="_blank"}와 비슷한 문제로, 짝수 번째 위치에 짝수 값을 홀수 번째 위치에 홀수 값으로 정렬하는 문제이다.
- 단, 각 홀수와 짝수 위치들 간 값의 크기에 대한 정렬은 상관 없다.

2. even과 odd는 짝수와 홀수 위치를 저장할 변수로, 시작 위치인 0과 1로 초기화한다.

3. even 혹은 odd가 nums의 길이 미만일 때 까지 아래를 반복한다.
- nums의 even번째 위치의 값이 짝수인 경우, even을 2 증가시킨다.
- 위가 아니라면 nums의 even번째 값과 odd번째 값을 바꾸고 odd를 2 증가시킨다.

4. 반복이 완료되면 주어진 조건대로 정렬된 nums 배열을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortArrayByParityII.java){:target="_blank"}에서 확인 가능합니다.