---
title: "Leetcode Java Check If It Is a Good Array"
excerpt: "Leetcode - 'Check If It Is a Good Array' 문제 Java 풀이"
last_modified_at: 2025-04-01T19:50:00
header:
  image: /assets/images/leetcode/check-if-it-is-a-good-array.png
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
[Link](https://leetcode.com/problems/check-if-it-is-a-good-array/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isGoodArray(int[] nums) {
    int result = nums[0];
    for (int num : nums) {
      while (num > 0) {
        int temp = result % num;
        result = num;
        num = temp;
      }
      if (result == 1) {
        return true;
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/check-if-it-is-a-good-array/submissions/1592999727/){:target="_blank"}

# 설명
1. nums 내 아래의 규칙을 만족하는 부분 배열이 존재하는지 검증하는 문제이다.
- 부분 배열 내 각 값을 임의 정수와 곱한 값을 합한 값이 1이 된다.

2. result에 nums의 첫 값을 먼저 넣어준다.

3. nums의 값을 순차적으로 num에 넣어 아래를 반복한다.
- num이 0보다 클 때까지, temp에 result와 num을 나눈 나머지 값을 임시 보관 후 result에 num을 num에 temp를 넣어준다.
- 위 반복이 완료된 후 result가 1인 조건을 만족하는 부분 집합이 되는 경우, true를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 조건을 만족하는 부분 배열이 존재하지 않으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CheckIfItIsAGoodArray.java){:target="_blank"}에서 확인 가능합니다.