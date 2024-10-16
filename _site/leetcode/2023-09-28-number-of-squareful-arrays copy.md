---
title: "Leetcode Java Sort Array By Parity"
excerpt: "Leetcode Sort Array By Parity Java"
last_modified_at: 2023-09-28T10:20:00
header:
  image: /assets/images/leetcode/sort-array-by-parity.png
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
[Link](https://leetcode.com/problems/sort-array-by-parity){:target="_blank"}

# 코드
```java
class Solution {

  public int[] sortArrayByParity(int[] nums) {
    for (int i = 0, j = 0; j < nums.length; j++) {
      if (nums[j] % 2 == 0) {
        int temp = nums[i];
        nums[i++] = nums[j];
        nums[j] = temp;
      }
    }
    return nums;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/sort-array-by-parity/submissions/1060961489/){:target="_blank"}

# 설명
1. nums의 짝수 값을 배열 앞으로, 홀수 값을 배열 뒤로 이동시키는 문제이다.

2. i와 j는 홀수와 짝수 값의 위치를 저장할 변수로, 둘 다 0으로 초기화 시키고 j가 nums의 길이 미만까지 증가시키며 아래를 반복한다.
- nums[j]의 값이 짝수인 경우, i와 j의 값의 위치를 바꿔준다.

3. 반복이 완료되면 정렬된 nums를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortArrayByParity.java){:target="_blank"}에서 확인 가능합니다.