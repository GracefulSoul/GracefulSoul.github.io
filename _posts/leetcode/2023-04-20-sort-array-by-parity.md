---
title: "Leetcode Java Fruit Into Baskets"
excerpt: "Leetcode - 'Fruit Into Baskets' 문제 Java 풀이"
last_modified_at: 2023-04-20T18:50:00
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
[Link](https://leetcode.com/problems/sort-array-by-parity/submissions/936831244/){:target="_blank"}

# 설명
1. 정수 배열인 nums의 앞 부분에는 짝수, 뒷 부분에는 홀수로 아무 순서로 정렬 후 반환하는 문제이다.

2. 0부터 nums의 길이 미만까지 j를 증가시키고, i를 0으로 초기화하여 아래를 반복한다.
- nums의 j번째 값이 짝수인 경우, i번째 값과 j번째 값을 바꾸고 i를 증가시킨다.

3. 반복이 완료되어 정렬된 nums를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SortArrayByParity.java){:target="_blank"}에서 확인 가능합니다.