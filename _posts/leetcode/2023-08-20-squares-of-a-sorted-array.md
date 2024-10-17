---
title: "Leetcode Java Squares of a Sorted Array"
excerpt: "Leetcode Easy - 'Squares of a Sorted Array' 문제 Java 풀이"
last_modified_at: 2023-08-20T11:00:00
header:
  image: /assets/images/leetcode/squares-of-a-sorted-array.png
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
[Link](https://leetcode.com/problems/squares-of-a-sorted-array){:target="_blank"}

# 코드
```java
class Solution {

  public int[] sortedSquares(int[] nums) {
    int length = nums.length;
    int[] result = new int[length];
    int i = 0;
    int j = length - 1;
    int k = length - 1;
    while (i <= j) {
      if (Math.abs(nums[i]) > Math.abs(nums[j])) {
        result[k] = nums[i] * nums[i];
        i++;
      } else {
        result[k] = nums[j] * nums[j];
        j--;
      }
      k--;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/squares-of-a-sorted-array/submissions/1026245883/){:target="_blank"}

# 설명
1. nums의 모든 값을 제곱으로 변환하여 오름차순 정렬하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 결과인 제곱으로 변환한 값을 오름차순으로 넣어줄 변수로, length 길이의 정수 배열로 초기화한다.
- i와 j는 nums의 시작과 종료 위치를 저장할 변수로, 0과 $length - 1$로 초기화한다.
- k는 result의 위치를 저장할 변수로, 역순으로 넣기 위해 $length - 1$로 초기화한다.

3. i가 j 이하일 때 까지 아래를 반복한다.
- nums[i]를 제곱한 값이 nums[j]를 제곱한 값보다 큰 경우, result[k]에 nums[i]를 제곱한 값을 넣고 i를 증가시킨다.
- 위의 경우가 아니라면, result[k]에 nums[j]를 제곱한 값을 넣고 j를 감소시킨다.
- 다음 위치로 이동하기 위해 k를 감소시킨다.

4. 반복이 완료되면 조건에 만족하는 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SquaresOfASortedArray.java){:target="_blank"}에서 확인 가능합니다.