---
title: "Leetcode Java Contains Duplicate III"
excerpt: "Leetcode Contains Duplicate III Java 풀이"
last_modified_at: 2021-10-26T12:00:00
header:
  image: /assets/images/leetcode/contains-duplicate-iii.png
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
[Link](https://leetcode.com/problems/contains-duplicate-iii/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
    if (nums.length == 0 || k == 0) {
      return false;
    } else if (t == 0) {
      return this.containsNearbyDuplicate(nums, k);
    } else {
      Map<Long, Integer> map = new HashMap<>();
      for (int idx = 0; idx < nums.length; idx++) {
        Long key = (long)(nums[idx] / t) - (nums[idx] < 0 ? 1 : 0);
        if (map.get(key) != null
            || ((map.get(key - 1) != null && nums[idx] - map.get(key - 1) <= t))
            || ((map.get(key + 1) != null && map.get(key + 1) - nums[idx] <= t))) {
          return true;
        }
        map.put(key, nums[idx]);
        if (idx >= k) {
          map.remove((long) nums[idx - k] / t);
        }
      }
      return false;
    }
  }

  private boolean containsNearbyDuplicate(int[] nums, int k) {
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
[Link](https://leetcode.com/submissions/detail/577205027/){:target="_blank"}

# 설명
1. 지난 번 [Contains Duplicate II](../contains-duplicate-ii){:target="_blank"}와 비슷한 문제로, 주어진 배열 nums의 내부 값 중 임의 두 값의 차이가 t가 나는 값이 배열 내 k 거리안에 존재하는지를 확인하는 문제이다.

2. 주어진 배열 nums에 값이 없거나 k가 0인 경우, 문제 풀이가 불가능하므로 false를 주어진 문제의 결과로 반환한다.

3. t가 0인 경우 위에서 이야기한 지난 번 문제(Contains Duplicate II)와 동일한 문제이므로, 두 값의 동일한 값이 k번째에 있는지 검증 결과를 주어진 문제의 결과로 반환한다.

4. 그 외의 경우 아래를 통해 검증하고 해당 결과를 주어진 문제의 결과로 반환한다.
- 값을 임시로 저장하기 위해 map을 정의한다.
- 주어진 배열 nums를 반복하여 문제를 검증한다.
- key는 map의 key로 사용하기 위해 $\frac{nums[idx]}{t}$의 값에 음수인 경우 1을 빼준 값을 넣어준다.
- 아래 조건을 충족하면 true를 주어진 문제의 결과로 반환한다.
  - map에 key 값이 존재하면 두 값의 차이가 t 미만으로 조건을 충족한다.
  - $key - 1$의 값이 존재하고, $nums[idx] - map.get(key - 1)$의 값이 t 이하이면 nums[idx]의 값이 map에 있는 $key - 1$ 키의 값보다 크면서 두 값의 차이가 t 이하이므로 조건을 충족한다.
  - $key + 1$의 값이 존재하고, $map.get(key + 1) - nums[idx]$의 값이 t 이하이면 map에 있는 $key - 1$ 키의 값이 nums[idx]의 값보다 크면서 두 값의 차이가 t 이하이므로 조건을 충족한다.
- 위의 경우가 아니면, map에 key를 이용하여 nums[idx]의 값을 넣어준다.
- idx가 k보다 커지게 되면, map에서 조건 범위를 벗어나는 $\frac{nums[idx - k]}{t}$가 key인 값을 제거해준다.

5. 반복이 종료되면 해당 조건을 충족하지 못하므로 false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ContainsDuplicateIII.java){:target="_blank"}에서 확인 가능합니다.