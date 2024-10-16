---
title: "Leetcode Java Third Maximum Number"
excerpt: "Leetcode Third Maximum Number Java 풀이"
last_modified_at: 2022-03-14T12:00:00
header:
  image: /assets/images/leetcode/third-maximum-number.png
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
[Link](https://leetcode.com/problems/third-maximum-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int thirdMax(int[] nums) {
    long[] memory = new long[] { Long.MIN_VALUE, Long.MIN_VALUE, Long.MIN_VALUE };
    for (int num : nums) {
      if (num > memory[0]) {
        memory[2] = memory[1];
        memory[1] = memory[0];
        memory[0] = num;
      } else if (num < memory[0] && num > memory[1]) {
        memory[2] = memory[1];
        memory[1] = num;
      } else if (num < memory[1] && num > memory[2]) {
        memory[2] = num;
      }
    }
    return (int) (memory[2] == Long.MIN_VALUE ? memory[0] : memory[2]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/659543580/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums가 주어지면 중복되지 않은 세 번째 최댓값을 반환하는 문제이다.
- 세 번째 최댓값이 없는 경우, 최댓값을 반환한다.

2. 가장 큰 세 값을 저장하기 위한 memory를 overflow를 방지하기 위해 long 형의 배열로 정의하고, 각 자리에 Long의 가장 작은 값을 넣어준다.

3. nums의 모든 값을 반복하여 memory에 값을 넣어준다.
- num이 memory의 첫 번째 값보다 큰 경우, memory의 모든 값을 다음 위치로 이동시키고 첫 번째 자리에 num을 넣어준다.
- num이 memory의 첫 번째 값보다 작고 두 번째 값보다 큰 경우, memory의 두 번째 값부다 다음 위치로 이동시키고 두 번째 자리에 num을 넣어준다.
- num이 memory의 두 번째 값보다 작고 세 번째 값보다 큰 경우, memory의 세 번째 값에 num을 넣어준다.

4. memory의 세 번째 값이 초기값인지를 검증하여 아래를 수행한다.
- 위의 경우가 초기값인 경우, memory의 첫 값인 최댓 값을 int형으로 변환하여 주어진 문제의 결과로 반환한다.
- 위의 경우가 초기값이 아닌 경우, memory의 세 번째 값인 세 번째로 가장 큰 값을 int형으로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ThirdMaximumNumber.java){:target="_blank"}에서 확인 가능합니다.