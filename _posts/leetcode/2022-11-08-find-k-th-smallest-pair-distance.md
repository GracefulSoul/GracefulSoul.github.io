---
title: "Leetcode Java Find K-th Smallest Pair Distance"
excerpt: "Leetcode Find K-th Smallest Pair Distance Java"
last_modified_at: 2022-11-08T16:30:00
header:
  image: /assets/images/leetcode/find-k-th-smallest-pair-distance.png
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
[Link](https://leetcode.com/problems/find-k-th-smallest-pair-distance){:target="_blank"}

# 코드
```java
class Solution {

  public int smallestDistancePair(int[] nums, int k) {
    Arrays.sort(nums);
    int low = 0;
    int high = nums[nums.length - 1] - nums[0];
    while (low < high) {
      int mid = (low + high) / 2;
      int count = 0;
      for (int i = 0, j = 0; i < nums.length; i++) {
        while (nums[i] - nums[j] > mid) {
          j++;
        }
        count += i - j;
      }
      if (count >= k) {
        high = mid;
      } else {
        low = mid + 1;
      }
    }
    return low;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/839269230/){:target="_blank"}

# 설명
1. nums의 값들을 이용하여 k번째로 작은 거리를 반환하는 문제이다.
- a와 b의 거리는 두 값의 절대값의 차이로 정의된다.
- k번째로 작은 거리인 nums[i]의 값과 nums[j]의 값은, 0 < = i < j < nums.length를 만족한다.

2. nums의 모든 값들을 오름차순 정렬한다.

3. 최소 거리인 low에는 0을, 최대 거리인 high에는 nums의 마지막 값에서 첫 번째 값의 차이를 넣어준다.

4. low가 high 미만일 때 까지 아래를 반복한다.
- mid에 low와 high의 중간 값인 $\frac{low + high}{2}$을 넣어준다.
- count는 mid에 해당하는 거리 이하인 nums의 숫자 갯수를 넣을 변수로, 0으로 초기화한다.
- 0부터 nums의 길이 미만까지 i를 증가시키고, j는 0으로 아래를 반복한다.
  - $nums[i] - nums[j]$의 결과가 mid보다 클 때까지 j를 증가시켜준다.
  - count에 $i - j$를 더해서 mid 이하인 작은 거리 갯수를 계산한다.
- count가 k 이상인 경우, high에 mid를 넣어 범위를 낮은 수로 좁힌다.
- count가 k 미만인 경우, low에 $mid + 1$을 넣어 범위를 높은 수로 좁힌다.

5. 반복이 완료되면 k번째로 작은 거리인 low를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindKthSmallestPairDistance.java){:target="_blank"}에서 확인 가능합니다.