---
title: "Leetcode Java Largest Perimeter Triangle"
excerpt: "Leetcode Largest Perimeter Triangle Java"
last_modified_at: 2023-08-19T22:10:00
header:
  image: /assets/images/leetcode/largest-perimeter-triangle.png
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
[Link](https://leetcode.com/problems/largest-perimeter-triangle){:target="_blank"}

# 코드
```java
class Solution {

  public int largestPerimeter(int[] nums) {
    Arrays.sort(nums);
    for (int i = nums.length - 1; i > 1; i--) {
      if (nums[i - 2] + nums[i - 1] > nums[i]) {
        return nums[i - 2] + nums[i - 1] + nums[i];
      }
    }
    return 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/largest-perimeter-triangle/submissions/1025697960/){:target="_blank"}

# 설명
1. nums의 세 값을 이용하여 만들 수 있는 최대 크기의 삼각형의 세 변에 대한 합을 구하는 문제이다.
- 단, 만들 수 있는 삼각형이 없는 경우 0을 주어진 문제의 결과로 반환한다.

2. nums의 값들을 오름차순으로 정렬한다.

3. $nums.length - 1$부터 1 초과일 때 까지 i를 감소시키며 아래를 수행한다.
- nums의 $i - 2$번째 값과 $i - 1$ 값의 합이 i번째 값보다 큰 경우, 현재 위치에서 만들 수 있는 최대 크기의 삼각형이므로 세 값의 합을 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 nums의 값으로 삼각형을 만들 수 없으므로, 0을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestPerimeterTriangle.java){:target="_blank"}에서 확인 가능합니다.