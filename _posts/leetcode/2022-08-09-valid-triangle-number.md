---
title: "Leetcode Java Valid Triangle Number"
excerpt: "Leetcode Valid Triangle Number Java"
last_modified_at: 2022-08-09T12:40:00
header:
  image: /assets/images/leetcode/valid-triangle-number.png
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
[Link](https://leetcode.com/problems/valid-triangle-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int triangleNumber(int[] nums) {
    if (nums.length < 3) {
      return 0;
    }
    Arrays.sort(nums);
    int count = 0;
    for (int idx = 2; idx < nums.length; idx++) {
      int left = 0;
      int right = idx - 1;
      while (left < right) {
        if (nums[left] + nums[right] > nums[idx]) {
          count += right - left;
          right--;
        } else {
          left++;
        }
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/768961421/){:target="_blank"}

# 설명
1. nums의 값들을 이용하여 삼각형을 만들 수 있는 경우의 수를 구하는 문제이다.

2. nums의 길이가 3 미만인 경우, 삼각형을 만들 수 없으므로 0을 주어진 문제의 결과로 반환한다.

3. nums의 값들을 오름차순으로 정렬한다.

4. count는 만들 수 있는 삼각형의 개수를 저장할 변수로, 0으로 초기화한다.

5. 2부터 nums의 길이 미만까지 idx를 증가시키며 아래를 반복한다.
- left에 0, right에 $idx - 1$을 넣어 탐색 위치를 초기화한다.
- left가 right 미만일 때까지 반복하여 아래를 수행한다.
  - nums의 left번째 값과 right번째 값의 합이 idx번째 값보다 큰 경우 삼각형을 만들 수 있으므로, 앞의 조합으로 만들 수 있는 조합의 수인 $right - left$ 값을 count에 더해주고 right를 감소시켜 범위를 축소시킨다.
  - 위의 경우가 아니면 삼각형을 만들 수 없으므로, left를 증가시켜 범위를 축소시킨다.

6. 반복이 완료되면 경우의 수를 저장한 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ValidTriangleNumber.java){:target="_blank"}에서 확인 가능합니다.