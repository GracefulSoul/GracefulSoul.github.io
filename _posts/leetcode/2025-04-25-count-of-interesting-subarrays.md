---
title: "Leetcode Java Count of Interesting Subarrays"
excerpt: "Leetcode - 'Count of Interesting Subarrays' 문제 Java 풀이"
last_modified_at: 2025-04-25T19:15:00
header:
  image: /assets/images/leetcode/count-of-interesting-subarrays.png
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
[Link](https://leetcode.com/problems/count-of-interesting-subarrays/){:target="_blank"}

# 코드
```java
class Solution {

  public long countInterestingSubarrays(List<Integer> nums, int modulo, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, 1);
    long result = 0;
    int sum = 0;
    for (int num : nums) {
      sum = (sum + (num % modulo == k ? 1 : 0)) % modulo;
      result += map.getOrDefault((sum - k + modulo) % modulo, 0);
      map.put(sum, map.getOrDefault(sum, 0) + 1);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-of-interesting-subarrays/submissions/1617466371/){:target="_blank"}

# 설명
1. nums 내 아래 규칙을 만족하는 연속된 부분 배열의 갯수를 계산하는 문제이다.
- 부분 배열인 [l, r] 범위 내 nums[i] % modulo = k를 만족하는 값의 갯수인 cnt도 cnt % modulo = k를 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 갯수를 계산하기 위한 변수로, HashMap으로 초기화 후 키가 0인 위치에 값을 1로 넣어준다.
- result는 부분 배열의 갯수를 계산할 변수로, 0으로 초기화한다.
- sum은 부분 합계를 저장할 변수로, 0으로 초기화한다.

3. nums의 값들을 순차적으로 num에 넣어 아래를 수행한다.
- sum에 num % modulo의 결과가 k인 조건을 만족하면 1을, 아니면 0을 sum에 더한 값을 modulo로 나눈 나머지 값을 넣어준다.
- result에 map에서 $sum - k + modulo$의 값을 modulo로 나눈 값에 해당하는 키의 값을 가져와 더해준다.
- map에서 sum이 키의 값을 1 증가시켜준다.

4. 반복이 완료되면 부분 배열의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 해설
- $sum - k + modulo$에서 modulo는 $sum - k$가 음수인 경우를 방지하기 위한 값이므로, 아래부터는 $sum - k$에 대해서 이야기한다.
- map에서 $sum - k$의 값을 modulo로 나눈 나머지 값에 해당하는 키의 값이 조건을 만족하는 부분 배열의 갯수인 이유는 아래와 같다.
  - 부분 배열 [i, j]이 cnt % modulo = k를 만족할 때, nums[i] % modulo = k를 만족하는 숫자의 갯수를 계산할 sum() 함수를 사용해 l = sum(0, $i - 1$), r = sum(0, j)로 $r - l$ = sum(i, j)을 만족한다.
  - 위를 기반으로 ($r - l$) % modulo = k를 만족할 때, modulo를 각 값에 적용하면 (r % modulo) - (l % modulo) = k를 만족한다.
  - k % modulo = k를 만족하므로, (r % modulo) - (l % modulo) = k % modulo가 성립한다.
  - (l % modulo) - (k % modulo)를 좌우 변에 더해주면, (r % modulo) - (k % modulo) = l % modulo가 되고, 이는 (r - k) % modulo = l % modulo가 된다.
  - 즉, $sum - k$는 두 조건을 만족하는 키를 뜻하고 이에 대한 값은 조건을 만족하는 부분 배열의 갯수가 된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountOfInterestingSubarrays.java){:target="_blank"}에서 확인 가능합니다.