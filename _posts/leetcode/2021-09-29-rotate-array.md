---
title: "Leetcode Java Rotate Array"
excerpt: "Leetcode - 'Rotate Array' 문제 Java 풀이"
last_modified_at: 2021-09-29T12:00:00
header:
  image: /assets/images/leetcode/rotate-array.png
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
[Link](https://leetcode.com/problems/rotate-array/){:target="_blank"}

# 코드
```java
class Solution {

  public void rotate(int[] nums, int k) {
    k %= nums.length;
    this.reverse(nums, 0, nums.length - 1);
    this.reverse(nums, 0, k - 1);
    this.reverse(nums, k, nums.length - 1);
  }

  private void reverse(int[] nums, int start, int end) {
    while (start < end) {
      int temp = nums[start];
      nums[start++] = nums[end];
      nums[end--] = temp;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/562704277/){:target="_blank"}

# 설명
1. 주어진 배열인 nums를 k번 값을 뒤에 있는 값을 앞으로 오게 회전하는 문제이다.

2. k에 nums.length로 나눈 나머지를 넣어준다.
- nums를 nums.length번 회전하면 같은 위치이므로, 횟수를 줄여준다.

3. 세 번 배열의 값들을 반전시킴으로써 원하는 배열의 형태를 만들어준다.
- nums를 처음 값부터 마지막 값까지 반전시킨다.
- nums를 처음 값부터 $k - 1$ 번째 위치의 값까지 반전시킨다.
- nums를 k 번째 위치의 값부터 마지막 값까지 반전시킨다.
  - 세 번의 반전을 통해서 k번 회전시킨 결과와 동일하게 된다.
  - nums가 [1, 2, 3, 4, 5] & k가 3의 경우를 예를 든다.
    - 기본 회전의 경우, [5, 1, 2, 3, 4] -> [4, 5, 1, 2, 3] -> [3, 4, 5, 1, 2]
    - 위의 반전의 경우, [5, 4, 3, 2, 1] -> [3, 4, 5, 2, 1] -> [3, 4, 5, 1, 2]

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RotateArray.java){:target="_blank"}에서 확인 가능합니다.