---
title: "Leetcode Java Make Sum Divisible by P"
excerpt: "Leetcode Make Sum Divisible by P Java"
last_modified_at: 2024-10-03T10:20:00
header:
  image: /assets/images/leetcode/make-sum-divisible-by-p.png
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
[Link](https://leetcode.com/problems/make-sum-divisible-by-p/){:target="_blank"}

# 코드
```java
class Solution {

  public int minSubarray(int[] nums, int p) {
    int remainder = 0;
    for (int num : nums) {
      remainder = (remainder + num) % p;
    }
    if (remainder == 0) {
      return 0;
    }
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, -1);
    int length = nums.length;
    int min = length;
    int curr = 0;
    for (int i = 0; i < length; i++) {
      curr = (curr + nums[i]) % p;
      map.put(curr, i);
      min = Math.min(min, i - map.getOrDefault((curr - remainder + p) % p, -length));
    }
    return min < length ? min : -1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/make-sum-divisible-by-p/submissions/1409943523/){:target="_blank"}

# 설명
1. nums의 모든 값의 합이 p가 되도록 nums 내 연속된 값들을 제거하기 위한 최소 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- remainder에 nums 모든 값을 더하면서 p를 나눈 나머지 값을 넣어주고, 0인 경우 합이 p로 나누어 떨어지므로 주어진 문제의 결과로 0을 반환한다.
- map은 값과 위치를 저장할 변수로, HashMap으로 초기화하고 키가 0인 값에 -1을 넣어준다.
- length는 nums의 길이를 저장한 변수이다.
- min은 최소 갯수를 계산할 변수로, 가능한 큰 갯수인 length로 초기화한다.
- curr은 현재까지 부족한 값을 저장할 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키면서 아래를 반복한다.
- curr에 $curr + nums[i]$의 값에 p를 나눈 나머지 값을 넣어준다.
- map의 curr이 키인 위치에 i를 넣어 해당 위치에 부족한 값을 저장한다.
- min에 min과 i에 map 내 $curr - remainer + p$를 p로 나눈 나머지 위치의 값 혹은 값이 없으면 -length를 빼준 값 중 작은 값을 넣어준다.

4. 반복이 완료되면 min이 length보다 작은 제거 가능한 숫자가 존재하면 min을, 아니면 불가능하므로 -1을 주어진 문제의 결과로 반환한다.

# 해설
- 제거할 숫자의 갯수를 탐색하기 위한 방법은 아래와 같다.
- 현재 위치인 i에서 $curr - remainer + p$를 p로 나눈 값이 키인 값의 위치 값을 빼면 그 사이 위치 값들을 제거한 갯수를 계산할 수 있다.
- 위의 경우가 아니라면 map 내 부족한 값에 대한 위치가 존재하지 않으므로, i에 nums의 숫자 갯수인 length를 더한 min보다 큰 값을 비교하여 min을 그대로 남겨준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MakeSumDivisibleByP.java){:target="_blank"}에서 확인 가능합니다.