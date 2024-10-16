---
title: "Leetcode Java Increasing Triplet Subsequence"
excerpt: "Leetcode Increasing Triplet Subsequence Java 풀이"
last_modified_at: 2022-01-10T13:00:00
header:
  image: /assets/images/leetcode/increasing-triplet-subsequence.png
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
[Link](https://leetcode.com/problems/increasing-triplet-subsequence/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean increasingTriplet(int[] nums) {
    int big = Integer.MAX_VALUE;
    int small = Integer.MAX_VALUE;
    for (int num : nums) {
      if (num <= small) {
        small = num;
      } else if (num < big) {
        big = num;
      } else if (num > big) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/616683654/){:target="_blank"}

# 설명
1. 주어진 nums를 이용하여 값이 증가하는 연속된 세 숫자가 존재하는지 검증하는 문제이다.
- 연속된 각 숫자 i, j, k는 i < j < k이며, nums[i] < nums[j] < nums[k]의 관계를 성립한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- big과 small은 위의 i와 k인 큰 값과 작은 값을 넣을 변수로, 각각 int형의 가장 큰 값을 넣어준다.

3. nums를 순회하여 검증을 수행한다.
- num이 small보다 작거나 같으면, small에 num을 넣어준다.
- 위의 경우가 아니면서 num이 big보다 작을 경우, big에 num을 넣어준다.
- 위의 경우들이 아니면서 num이 big보다 클 경우, true를 주어진 문제의 결과로 반환한다.

4. 반복이 종료되면 값이 증가하는 연속된 세 숫자가 없다는 의미이므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/IncreasingTripletSubsequence.java){:target="_blank"}에서 확인 가능합니다.