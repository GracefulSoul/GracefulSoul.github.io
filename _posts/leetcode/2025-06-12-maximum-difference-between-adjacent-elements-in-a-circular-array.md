---
title: "Leetcode Java Maximum Difference Between Adjacent Elements in a Circular Array"
excerpt: "Leetcode - 'Maximum Difference Between Adjacent Elements in a Circular Array' 문제 Java 풀이"
last_modified_at: 2025-06-12T19:20:00
header:
  image: /assets/images/leetcode/maximum-difference-between-adjacent-elements-in-a-circular-array.png
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
[Link](https://leetcode.com/problems/maximum-difference-between-adjacent-elements-in-a-circular-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxAdjacentDistance(int[] nums) {
    int length = nums.length;
    int result = this.getAbsoluteDifference(nums[0], nums[length - 1]);
    for (int i = 0; i < length - 1; i++) {
      result = Math.max(result, this.getAbsoluteDifference(nums[i], nums[i + 1]));
    }
    return result;
  }

  private int getAbsoluteDifference(int num1, int num2) {
    if (num1 > num2) {
      return num1 - num2;
    } else {
      return num2 - num1;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-difference-between-adjacent-elements-in-a-circular-array/submissions/1661792026/){:target="_blank"}

# 설명
1. 원형으로 순환하는 값들이 저장된 nums를 이용하여 인접한 두 값의 차이에 대한 절댓값이 최대인 값을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 인접한 두 값의 차이에 대한 절댓값이 최대인 값을 저장할 변수로, 첫 값과 마지막 값의 차이에 대한 절댓값으로 넣어준다.

3. 0부터 $length - 1$까지 i를 증가시키며 아래를 반복한다.
- result에 result의 값과 nums[i]의 값과 nums[$i + 1$]의 값의 차이에 대한 절댓값 중 큰 값을 저장한다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumDifferenceBetweenAdjacentElementsInACircularArray.java){:target="_blank"}에서 확인 가능합니다.