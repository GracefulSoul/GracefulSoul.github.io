---
title: "Leetcode Java Smallest Range II"
excerpt: "Leetcode Smallest Range II Java"
last_modified_at: 2023-04-27T20:00:00
header:
  image: /assets/images/leetcode/smallest-range-ii.png
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
[Link](https://leetcode.com/problems/smallest-range-ii){:target="_blank"}

# 코드
```java
class Solution {

  public int smallestRangeII(int[] nums, int k) {
    Arrays.sort(nums);
    int length = nums.length;
    int max = nums[length - 1];
    int min = nums[0];
    int result = max - min;
    for (int i = 0; i < length - 1; i++) {
      max = Math.max(max, nums[i] + (k * 2));
      min = Math.min(nums[i + 1], nums[0] + (k * 2));
      result = Math.min(result, max - min);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/smallest-range-ii/submissions/940559463/){:target="_blank"}

# 설명
1. 지난 번 [Smallest Range I](../smallest-range-i){:target="_blank"}과 유사하지만 이번에는 nums의 모든 값에 -k 혹은 k 값을 더했을 때, 최댓값과 최솟값의 차이가 가장 작은 값을 구하는 문제이다.

2. nums를 오름차순으로 정렬하고, 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- max와 min은 최댓값과 최솟값을 저장할 변수로, 정렬된 nums의 마지막 값인 가장 큰 값과 첫 값이 가장 작은 값으로 초기화한다.
- result는 결과를 저장할 변수로, 차이가 가장 큰 값인 max와 min의 차이로 초기화한다.

3. 0부터 $length - 1$까지 i를 증가시키며 아래를 수행한다.
- max에 이전 값까지 가장 큰 값인 max와 nums의 i번째 값에 -k 혹은 k를 더했을 때 발생 가능한 최대 차이인 $k \times 2$를 더한 값 중 큰 값을 넣어준다.
- min에 다음 값인 nums의 $i + 1$번째 값과 nums의 첫 값에 위와 동일하게 $k \times 2$를 더한 값 중 작은 값을 넣어준다.
- result에 result와 $max - min$의 결과 중 작은 값을 넣어준다.

4. 반복이 완료되면 최댓값과 최솟값의 차이가 가장 작은 값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SmallestRangeII.java){:target="_blank"}에서 확인 가능합니다.