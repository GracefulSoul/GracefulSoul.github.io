---
title: "Leetcode Java Total Hamming Distance"
excerpt: "Leetcode Total Hamming Distance Java 풀이"
last_modified_at: 2022-05-03T12:00:00
header:
  image: /assets/images/leetcode/total-hamming-distance.png
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
[Link](https://leetcode.com/problems/total-hamming-distance/){:target="_blank"}

# 코드
```java
class Solution {

  public int totalHammingDistance(int[] nums) {
    int count = 0;
    int length = nums.length;
    for (int j = 0; j < 32; j++) {
      int bitCount = 0;
      for (int num : nums) {
        bitCount += (num >> j) & 1;
      }
      count += bitCount * (length - bitCount);
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/691941983/){:target="_blank"}

# 설명
1. 지난번 [Hamming Distance](../hamming-distance){:target="_blank"} 문제와 유사한 문제로, 배열 내 정수들간 해밍 거리의 합을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 해밍 거리의 합을 저장할 변수로, 0으로 초기화한다.
- length는 num의 길이를 저장할 변수로, length의 길이로 초기화한다.

3. 0부터 int의 최대 비트의 수인 32 미만까지 j를 증가시키며 반복을 수행한다.
- 비트의 개수를 저장할 bitCount를 0으로 초기화한다.
- nums의 모든 숫자들을 반복하여 num의 비트를 j번 우측으로 이동시킨 값과 1을 AND(&) 비트 연산을 수행한 결과를 bitCount에 더해준다.
  - nums 내 모든 숫자의 비트 중 우측에서 j번째가 1이 되는 숫자의 개수를 bitCount에 넣어주는 것이다.
- count에 bitCount와 $length - bitCount$ 값의 곱을 더해준다.
  - 우측에서 j번째가 모두 동일한 경우 $length - bitCount = 0$으로, 해밍 거리의 합에서 제외된다.
  - 우측에서 j번째가 모두 동일하지 않은 경우, x개에 특정 비트가 있고 (length - x)개에 특정 비트가 없는 경우 $x \times (length - x)$개의 해밍 거리의 합이 계산된다.

4. 반복이 완료되면 해밍 거리의 합인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TotalHammingDistance.java){:target="_blank"}에서 확인 가능합니다.