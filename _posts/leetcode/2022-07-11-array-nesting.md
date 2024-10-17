---
title: "Leetcode Java Array Nesting"
excerpt: "Leetcode - 'Array Nesting' 문제 Java 풀이"
last_modified_at: 2022-07-11T21:00:00
header:
  image: /assets/images/leetcode/array-nesting.png
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
[Link](https://leetcode.com/problems/array-nesting/){:target="_blank"}

# 코드
```java
class Solution {

  public int arrayNesting(int[] nums) {
    int max = 0;
    for (int i = 0; i < nums.length; i++) {
      int length = 0;
      for (int j = i; nums[j] >= 0; length++) {
        int temp = nums[j];
        nums[j] = -1;
        j = temp;
      }
      max = Math.max(max, length);
    }
    return max;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/744206000/){:target="_blank"}

# 설명
1. 아래의 조건을 만족하는 집합의 가장 긴 길이를 구하는 문제이다.
- s[k] = {nums[k], nums[nums[k]], nums[nums[nums[k]]], ... }

2. 최대 길이를 저장할 max를 정의하고, 0으로 초기화한다.

3. 0부터 nums의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- 부분 길이를 저장할 length를 0으로 초기화 한다.
- i부터 nums[j]가 0 이상일 때 까지 j를 증가시키며 아래를 반복한다.
  - temp에 nums의 j번째 값을 넣어주고 nums의 j번째 값에 -1을 넣어 방문 기록을 남긴다.
  - j에 temp를 넣어준다.
- 반복이 완료되면 max에 max와 length중 큰 값을 넣어준다.

4. 반복이 완료되면 조건을 만족하는 가장 길 길이인 max를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ArrayNesting.java){:target="_blank"}에서 확인 가능합니다.