---
title: "Leetcode Java Count the Number of Good Subarrays"
excerpt: "Leetcode - 'Count the Number of Good Subarrays' 문제 Java 풀이"
last_modified_at: 2025-04-16T20:20:00
header:
  image: /assets/images/leetcode/count-the-number-of-good-subarrays.png
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
[Link](https://leetcode.com/problems/count-the-number-of-good-subarrays/){:target="_blank"}

# 코드
```java
class Solution {

  public long countGood(int[] nums, int k) {
    long result = 0L;
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0, j = 0; j < nums.length; j++) {
      int num = map.getOrDefault(nums[j], 0);
      k -= num;
      map.put(nums[j], num + 1);
      while (k <= 0) {
        map.put(nums[i], map.get(nums[i]) - 1);
        k += map.get(nums[i++]);
      }
      result += i;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-the-number-of-good-subarrays/submissions/1608465104/){:target="_blank"}

# 설명
1. 정수 배열인 nums을 이용하여 아래 규칙을 만족하는 부분 배열의 수를 반환하는 문제이다.
- 연속된 값들로 이루어진 부분 배열은 i < j, arr[i] == arr[j]를 만족하는 위치 값 (i, j)가 최소 k쌍 이상이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 부분 배열의 수를 계산할 변수로, 0으로 초기화한다.
- map은 nums[i] 기준의 조건을 만족하는 갯수를 계산하기 위한 변수로, HashMap으로 초기화한다.

3. i는 0으로 초기화하고, 0부터 nums의 길이 미만까지 j를 증가시키며 아래를 반복한다.
- num에 map에서 nums[j]의 값이 존재하면 해당 값을, 아니면 0을 넣어준다.
- k에 num인 조건에 해당하는 쌍의 갯수를 빼준 후, map에 nums[j]의 위치에 쌍의 갯수인 num을 1 증가시켜 넣어준다.
- k가 0 이하일 때 까지 아래를 반복하여 기존 쌍의 갯수를 차감하고 k를 원상복구시켜준다.
  - map의 nums[i]에 해당하는 위치에 해당 위치의 값에서 1을 빼준다.
  - k에 map에서 nums[i]에 해당하는 값을 가져와 더해준 후, i를 증가시켜준다.
- result에 i를 더해 부분 배열의 수를 더해준다.

4. 반복이 완료되면 계산된 부분 배열의 수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountTheNumberOfGoodSubarrays.java){:target="_blank"}에서 확인 가능합니다.