---
title: "Leetcode Java Type of Triangle"
excerpt: "Leetcode - 'Type of Triangle' 문제 Java 풀이"
last_modified_at: 2025-05-19T19:40:00
header:
  image: /assets/images/leetcode/type-of-triangle.png
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
[Link](https://leetcode.com/problems/type-of-triangle/){:target="_blank"}

# 코드
```java
class Solution {

  public String triangleType(int[] nums) {
    if (nums[0] + nums[1] <= nums[2] || nums[0] + nums[2] <= nums[1] || nums[1] + nums[2] <= nums[0]) {
      return "none";
    } else if (nums[0] == nums[1] && nums[1] == nums[2]) {
      return "equilateral";
    } else if (nums[0] == nums[1] || nums[1] == nums[2] || nums[0] == nums[2]) {
      return "isosceles";
    } else {
      return "scalene";
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/type-of-triangle/submissions/1638149520/){:target="_blank"}

# 설명
1. nums의 세 숫자를 이용하여 삼각형을 만들려고 할 때, 만들 수 있는 삼각형 종류를 반환하는 문제이다.
- 모든 변의 값이 동일한 삼각형은 정삼각형이라고 하며, "equilateral"를 반환한다.
- 두 변의 값이 동일한 삼각형은 이등변 삼각형이라고 하며, "isosceles"를 반환한다.
- 모든 변의 값이 다른 삼각형은 부등변 삼각형이라고 하며, "scalene"를 반환한다.
- 삼각형을 만들 수 없으면 "none"을 반환한다.

2. 아래의 각 상태에 따른 값을 반환한다.
- nums내 한 값이 나머지 두 값을 더한 값보다 작아 삼각형을 이룰 수 없는 경우, "none"을 반환한다.
- nums의 모든 값이 동일한 정삼각형을 만들 수 있는 경우, "equilateral"을 반환한다.
- nums의 임의 두 값이 동일한 이등변 삼각형을 만들 수 있는 경우, "isosceles"를 반환한다.
- 그 외인 부등변 삼각형을 만들 수 있는 경우, "scalene"을 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TypeOfTriangle.java){:target="_blank"}에서 확인 가능합니다.