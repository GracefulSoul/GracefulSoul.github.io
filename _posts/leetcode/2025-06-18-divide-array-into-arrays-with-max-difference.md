---
title: "Leetcode Java Divide Array Into Arrays With Max Difference"
excerpt: "Leetcode - 'Divide Array Into Arrays With Max Difference' 문제 Java 풀이"
last_modified_at: 2025-06-18T21:30:00
header:
  image: /assets/images/leetcode/divide-array-into-arrays-with-max-difference.png
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
[Link](https://leetcode.com/problems/divide-array-into-arrays-with-max-difference/){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] divideArray(int[] nums, int k) {
    Arrays.sort(nums);
    int length = nums.length;
    int[][] result = new int[length / 3][3];
    for (int i = 2; i < length; i += 3) {
      if (nums[i] - nums[i - 2] > k) {
        return new int[0][];
      } else {
        result[i / 3] = new int[] { nums[i - 2], nums[i - 1], nums[i] };
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/divide-array-into-arrays-with-max-difference/submissions/1668266654/){:target="_blank"}

# 설명
1. 3의 배수의 갯수의 정수가 존재하는 nums를 이용하여 부분 배열 내 값들의 차이는 k 이하를 만족하는 3개의 정수로 구성된 부분 배열들로 분리하는 문제이다.
- 단, 모든 값들을 부분 배열로 분리할 수 없으면 빈 배열을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의 혹은 초기화한다.
- nums를 오름차순으로 정렬한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 결과를 저장할 변수로, 가능한 부분 배열의 갯수인 $\frac{length}{3}$과 부분 배열의 길이인 3의 2차원 정수 배열로 초기화한다.

3. 2부터 length 미만까지 i를 3씩 증가시키며 아래를 반복한다.
- $nums[i] - nums[i - 2]$의 값이 k 초과인 조건을 만족하지 않는 경우, 빈 배열을 주어진 문제의 결과로 반환한다.
- 위의 경우가 아니라면 result[$\frac{i}{3}$]의 위치에 nums[$i - 2$], nums[$i - 1$], num[i]의 값을 넣어준다.

4. 반복이 완료되어 조건을 만족하는 배열로 구성된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DivideArrayIntoArraysWithMaxDifference.java){:target="_blank"}에서 확인 가능합니다.