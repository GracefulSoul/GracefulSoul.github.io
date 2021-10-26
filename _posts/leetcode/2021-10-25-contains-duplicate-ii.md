---
title: "Leetcode Java Contains Duplicate II"
excerpt: "Leetcode Contains Duplicate II Java 풀이"
last_modified_at: 2021-10-25T13:00:00
header:
  image: /assets/images/leetcode/contains-duplicate-ii.png
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
[Link](https://leetcode.com/problems/contains-duplicate-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean containsNearbyDuplicate(int[] nums, int k) {
    Set<Integer> set = new HashSet<>();
    for (int idx = 0; idx < nums.length; idx++) {
      if (idx > k) {
        set.remove(nums[idx - k - 1]);
      }
      if (!set.add(nums[idx])) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/576785901/){:target="_blank"}

# 설명
1. 주어진 배열 nums의 내부 값 중 임의 동일한 두 값이 배열 내 k 거리안에 존재하는지를 확인하는 문제이다.

2. k번째 거리까지 값을 넣어 검증에 사용하기 위한 set을 정의한다.

3. 반복을 통해 nums의 모든 값을 탐색하여 1번에서 이야기한 조건에 충족하는지를 검증한다.
- idx가 k보다 크게 되면 조건의 범위에서 벗어난 nums[$idx - k - 1$] 값을 set에서 제거한다.
- set에 nums[idx] 값을 추가할 때 해당 값이 set에 존재하는 경우, true를 주어진 문제의 결과로 반환한다.

4. 반복이 끝나면 조건에 충족한 값이 존재하지 않으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ContainsDuplicateII.java){:target="_blank"}에서 확인 가능합니다.