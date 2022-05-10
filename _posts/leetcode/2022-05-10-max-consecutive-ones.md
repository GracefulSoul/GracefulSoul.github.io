---
title: "Leetcode Java Max Consecutive Ones"
excerpt: "Leetcode Max Consecutive Ones Java 풀이"
last_modified_at: 2022-05-10T18:00:00
header:
  image: /assets/images/leetcode/max-consecutive-ones.png
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
[Link](https://leetcode.com/problems/max-consecutive-ones/){:target="_blank"}

# 코드
```java
class Solution {

  public int findMaxConsecutiveOnes(int[] nums) {
    int max = 0;
    int curr = 0;
    for (int num : nums) {
      if (num == 0) {
        max = Math.max(max, curr);
        curr = 0;
      } else {
        curr++;
      }
    }
    return Math.max(max, curr);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/696539387/){:target="_blank"}

# 설명
1. nums 내 연속된 1의 갯수가 가장 긴 결과를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 연속된 1의 갯수가 가장 긴 결과를 저장할 변수로, 0으로 초기화한다.
- curr은 현재 1의 갯수가 몇 개 연속되었는지 저장할 변수로, 0으로 초기화한다.

3. nums 내 모든 값들을 반복하여 아래를 수행한다.
- num이 0인 경우, max와 curr 중 가장 큰 값을 max에 넣어주고 curr을 0으로 초기화한다.
- num이 0이 아닌 경우, curr을 증가시킨다.

4. 마지막 전 까지 연속된 1의 갯수가 가장 긴 max와 마지막으로 연속된 1의 갯수인 curr 중 가장 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxConsecutiveOnes.java){:target="_blank"}에서 확인 가능합니다.