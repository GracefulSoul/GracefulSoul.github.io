---
title: "Leetcode Java Monotonic Array"
excerpt: "Leetcode Monotonic Array Java"
last_modified_at: 2023-04-08T11:20:00
header:
  image: /assets/images/leetcode/monotonic-array.png
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
[Link](https://leetcode.com/problems/monotonic-array){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isMonotonic(int[] nums) {
    if (nums.length > 2) {
      boolean increase = true;
      boolean decrease = true;
      for (int i = 1; i < nums.length; i++) {
        if (nums[i - 1] > nums[i]) {
          increase = false;
        } else if (nums[i - 1] < nums[i]) {
          decrease = false;
        }
        if (!decrease && !increase) {
          return false;
        }
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/monotonic-array/submissions/929910430/){:target="_blank"}

# 설명
1. 배열이 단조롭게 증가하거나 감소하는지 검증하는 문제이다.
- 배열의 모든 값이 점층적으로 증가하면 단조롭게 증가하는 배열이고, 점층적으로 감소하면 단조롭게 감소하는 배열이다.

2. nums의 길이가 2 이하인 경우 무조건 단조로운 배열이므로, true를 주어진 문제의 결과로 반환한다.

3. increase와 decrease는 단조롭게 증가하고 감소하는지 검증하는 변수로, true로 초기화한다.

4. 1부터 nums의 길이 미만까지 i를 증가시키며 아래를 검증한다.
- nums의 $i - 1$번째 값이 i번째 값보다 큰 경우, 단조롭게 증가하지 않으므로 increase를 false로 변경한다.
- nums의 $i - 1$번째 값보다 i번째 값이 큰 경우, 단조롭게 감소하지 않으므로 decrease를 false로 변경한다.
- decrease와 increase 값이 둘 다 false인 경우, 단조로운 배열이 될 수 없으므로 false를 주어진 문제의 결과로 반환한다.

5. 반복이 완료되면 단조로운 배열로 검증되었으므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MonotonicArray.java){:target="_blank"}에서 확인 가능합니다.