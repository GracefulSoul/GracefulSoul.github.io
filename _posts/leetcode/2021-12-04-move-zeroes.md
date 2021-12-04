---
title: "Leetcode Java Move Zeroes"
excerpt: "Leetcode Move Zeroes Java 풀이"
last_modified_at: 2021-12-04T12:00:00
header:
  image: /assets/images/leetcode/move-zeroes.png
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
[Link](https://leetcode.com/problems/move-zeroes/){:target="_blank"}

# 코드
```java
class Solution {

  public void moveZeroes(int[] nums) {
    int idx = 0;
    for (int num : nums) {
      if (num != 0) {
        nums[idx++] = num;
      }
    }
    while (idx < nums.length) {
      nums[idx++] = 0;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/596639075/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums 내 0을 해당 배열 내 마지막 위치로 이동시키는 문제이다.

2. nums 배열 내 0이 아닌 값들을 차례대로 넣기 위해 idx를 0으로 정의한다.

3. nums를 반복하여 0이 아닐 때 까지 nums[idx]에 넣고 idx를 증가시킨다.

4. 0이 아닌 값들을 차례대로 넣은 nums의 idx 이후 값들을 모두 0으로 채워준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MoveZeroes.java){:target="_blank"}에서 확인 가능합니다.