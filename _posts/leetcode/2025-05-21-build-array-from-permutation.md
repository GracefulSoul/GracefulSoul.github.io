---
title: "Leetcode Java Build Array from Permutation"
excerpt: "Leetcode - 'Build Array from Permutation' 문제 Java 풀이"
last_modified_at: 2025-05-21T20:00:00
header:
  image: /assets/images/leetcode/build-array-from-permutation.png
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
[Link](https://leetcode.com/problems/build-array-from-permutation/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] buildArray(int[] nums) {
    int length = nums.length;
    int[] result = new int[length];
    for (int i = 0; i < length; i++) {
      result[i] = nums[nums[i]];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/build-array-from-permutation/submissions/1640220633/){:target="_blank"}

# 설명
1. nums 내 값들을 nums 내 값에 해당하는 위치 값을 넣어 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 결과 값을 넣을 배열로, length 길이의 정수 배열로 초기화한다.

3. 0부터 length까지 i를 증가시키며, result[i]의 위치에 nums[nums[i]]의 값을 순차적으로 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BuildArrayFromPermutation.java){:target="_blank"}에서 확인 가능합니다.