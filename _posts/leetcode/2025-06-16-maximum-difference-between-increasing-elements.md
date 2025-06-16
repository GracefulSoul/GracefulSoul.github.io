---
title: "Leetcode Java Maximum Difference Between Increasing Elements"
excerpt: "Leetcode - 'Maximum Difference Between Increasing Elements' 문제 Java 풀이"
last_modified_at: 2025-06-15T11:20:00
header:
  image: /assets/images/leetcode/maximum-difference-between-increasing-elements.png
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
[Link](https://leetcode.com/problems/maximum-difference-between-increasing-elements/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumDifference(int[] nums) {
    int result = -1;
    int min = nums[0];
    for (int i = 1; i < nums.length; i++) {
      result = Math.max(result, nums[i] - min);
      min = Math.min(min, nums[i]);
    }
    return result == 0 ? -1 : result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-difference-between-increasing-elements/submissions/1665894613/){:target="_blank"}

# 설명
1. nums를 이용하여 $0 <= i < j < n$를 만족하는 i와 j로 $nums[i] - nums[j]$ 결과가 최대인 값을 반환하는 문제이다.
- 조건을 만족하는 i와 j가 없는 경우, -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과값을 저장할 변수로, 불가능한 -1로 초기화한다.
- min은 최솟값을 저장할 변수로, nums[0] 값으로 초기화한다.

3. 1부터 num의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- result에 result 와 $nums[i] - min$인 두 값의 최대 차잇값을 넣어준다.
- min에 이전까지 최솟값인 min과 num[i] 중 가장 작은 값을 넣어준다.

4. result가 0인 차잇값이 없으면 -1을, 아니면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumDifferenceBetweenIncreasingElements.java){:target="_blank"}에서 확인 가능합니다.