---
title: "Leetcode Java Count Equal and Divisible Pairs in an Array"
excerpt: "Leetcode - 'Count Equal and Divisible Pairs in an Array' 문제 Java 풀이"
last_modified_at: 2025-04-17T18:30:00
header:
  image: /assets/images/leetcode/count-equal-and-divisible-pairs-in-an-array.png
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
[Link](https://leetcode.com/problems/count-equal-and-divisible-pairs-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int countPairs(int[] nums, int k) {
    int length = nums.length;
    int result = 0;
    for (int i = 0; i < length - 1; i++) {
      for (int j = i + 1; j < length; j++) {
        if (nums[i] == nums[j] && i * j % k == 0) {
          result++;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-equal-and-divisible-pairs-in-an-array/submissions/1609384126/){:target="_blank"}

# 설명
1. 정수 배열 nums를 이용하여 아래 조건을 만족하는 쌍의 갯수를 계산하는 문제이다.
- 0 <= i < j < n를 만족하는 i와 j를 선택할 때, nums[i] == nums[j]와 $i \times j$의 값이  k의 배수를 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 조건을 만족하는 쌍의 갯수를 계산할 변수로, 0으로 초기화한다.

3. 0부터 $length - 1$까지 i를 증가시키고, $i + 1$부터 length 미만까지 j를 증가시키며 아래를 반복한다.
- nums[i] == nums[j]를 만족하면서 $i \times j$의 값이 k의 배수인 경우, result를 증가시킨다.

4. 반복이 완료되면 조건을 만족하는 쌍의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountEqualAndDivisiblePairsInAnArray.java){:target="_blank"}에서 확인 가능합니다.