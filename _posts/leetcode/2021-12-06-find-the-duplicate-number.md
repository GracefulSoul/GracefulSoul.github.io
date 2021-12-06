---
title: "Leetcode Java Find the Duplicate Number"
excerpt: "Leetcode Find the Duplicate Number Java 풀이"
last_modified_at: 2021-12-06T13:00:00
header:
  image: /assets/images/leetcode/find-the-duplicate-number.png
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
[Link](https://leetcode.com/problems/find-the-duplicate-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int findDuplicate(int[] nums) {
    int memory[] = new int[nums.length];
    for (int num : nums) {
      memory[num]++;
    }
    for (int num : nums) {
      if (memory[num] > 1) {
        return num;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/597633320/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums 중 중복된 값이 있는지 찾아 반환하는 문제이다.
- 배열 내 값은 nums의 크기보다 작은 수로 이루어져 있다.
- 해당 정수 배열 내 무조건 하나의 정수만 2번 혹은 그 이상 발생한다.

2. memory 배열을 nums의 크기만큼 정의한다.

3. nums를 반복하여 momory[num] 위치의 값을 증가시킨다.

4. nums를 반복하여 memory[num]의 값이 1보다 큰 경우, num을 주어진 문제의 결과로 반환한다.

5. 그 외의 경우, 기본 조건에 의해 발생되지 않겠지만 반드시 반환문이 필요하므로 -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindTheDuplicateNumber.java){:target="_blank"}에서 확인 가능합니다.