---
title: "Leetcode Java Subarray Sum Equals K"
excerpt: "Leetcode Subarray Sum Equals K Java"
last_modified_at: 2022-07-06T19:30:00
header:
  image: /assets/images/leetcode/subarray-sum-equals-k.png
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
[Link](https://leetcode.com/problems/subarray-sum-equals-k/){:target="_blank"}

# 코드
```java
class Solution {

  public int subarraySum(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    int sum = 0;
    int count = 0;
    map.put(0, 1);
    for (int num : nums) {
      sum += num;
      if (map.containsKey(sum - k)) {
        count += map.get(sum - k);
      }
      map.put(sum, map.getOrDefault(sum, 0) + 1);
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/739951495/){:target="_blank"}

# 설명
1. nums의 연속된 요소의 합이 k인 부분 배열의 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 부분 합을 이용한 갯수를 저장할 변수로, HashMap으로 초기화하고 키가 0인 값을 1로 초기화한다.
- sum은 부분 합을 저장할 변수로, 0으로 초기화한다.
- count는 k가 되는 부분 배열의 갯수를 저장할 변수로, 0으로 초기화한다.

3. nums의 모든 요소를 num에 넣어 반복한다.
- sum에 num을 더해 합계를 계산한다.
- map에 $sum - k$이 키인 값이 존재하면, count에 map에서 $sum - k$인 값을 더해 부분 배열의 합이 k인 갯수를 증가시킨다.
- map에 키가 sum인 값을 1 증가시키고 반복을 계속 수행한다.

4. 반복이 완료되면 부분 배열의 갯수를 저장한 count를 주어진 문제의 결과로 반환한다.

# 해설
- nums의 [0, $i - 1$] 구간의 합과 [0, j] 구간의 합을 알면 [i, j] 구간의 합을 알 수 있다.
- 그러므로 map에 sum에 해당하는 값을 증가시키고, 다음 차례에서 $sum - k$의 값이 존재하면 count에 누적시키면 연속된 요소를 이용한 부분 배열의 합이 k인 갯수를 구할 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SubarraySumEqualsK.java){:target="_blank"}에서 확인 가능합니다.