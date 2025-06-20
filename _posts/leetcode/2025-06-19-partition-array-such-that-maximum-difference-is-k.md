---
title: "Leetcode Java Divide Array Into Arrays With Max Difference"
excerpt: "Leetcode - 'Divide Array Into Arrays With Max Difference' 문제 Java 풀이"
last_modified_at: 2025-06-19T22:30:00
header:
  image: /assets/images/leetcode/partition-array-such-that-maximum-difference-is-k.png
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
[Link](https://leetcode.com/problems/partition-array-such-that-maximum-difference-is-k/){:target="_blank"}

# 코드
```java
class Solution {

  public int partitionArray(int[] nums, int k) {
    Arrays.sort(nums);
    int result = 1;
    for (int i = 1, j = 0; i < nums.length; i++) {
      if (nums[i] - nums[j] > k) {
        result++;
        j = i;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/partition-array-such-that-maximum-difference-is-k/submissions/1669446465/){:target="_blank"}

# 설명
1. 정수 배열인 nums를 최댓값과 최솟값의 차이가 최대 k가 되도록 나눌 수 있는 최소 부분 배열의 갯수를 구하는 문제이다.

2. nums의 값을 오름차순 정렬하고, 결과를 저장할 변수인 result를 1로 초기화한다.

3. 1부터 nums의 길이 미만까지 i를 증가시키고, j는 0으로 초기화 하여 아래를 반복한다.
- $nums[i] - nums[j]$의 값이 k 초과인 경우, result를 증가시키고 시작 위치를 저장할 j에 현재 위치인 i를 넣어준다.

4. 반복이 완료되면 최소 부분 배열의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PartitionArraySuchThatMaximumDifferenceIsK.java){:target="_blank"}에서 확인 가능합니다.