---
title: "Leetcode Java Minimum Operations to Make Binary Array Elements Equal to One I"
excerpt: "Leetcode - 'Minimum Operations to Make Binary Array Elements Equal to One I' 문제 Java 풀이"
last_modified_at: 2025-03-19T19:00:00
header:
  image: /assets/images/leetcode/minimum-operations-to-make-binary-array-elements-equal-to-one-i.png
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
[Link](https://leetcode.com/problems/minimum-operations-to-make-binary-array-elements-equal-to-one-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int minOperations(int[] nums) {
    int length = nums.length;
    int count = 0;
    for (int i = 0; i <= length - 3; i++) {
      if (nums[i] == 0) {
        nums[i] ^= 1;
        nums[i + 1] ^= 1;
        nums[i + 2] ^= 1;
        count++;
      }
    }
    return nums[length - 1] == 0 || nums[length - 2] == 0 ? -1 : count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-operations-to-make-binary-array-elements-equal-to-one-i/submissions/1578917356/){:target="_blank"}

# 설명
1. 0과 1로 이루어진 이진 정수 배열 nums의 연속된 세 정수의 값을 플립(0에서 1 혹은 1에서 0)하여 모든 값을 1로 만들기 위한 최소 연산의 수를 구하는 문제이다.
- 단, 모든 값을 1로 만들 수 없다면 -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- count는 최소 연산 횟수를 구하기 위한 변수로, 0으로 초기화한다.

3. 0부터  $length - 3$ 이하까지 i를 증가시키며 아래를 반복한다.
- nums[i]의 값이 0인 경우, 해당 위치 값을 포함한 연속된 세 값을 각자 1과 XOR 비트 연산을 수행한 값을 넣어주고 count를 증가시켜준다.

4. 반복이 완료되면, 마지막 두 값이 0이면 -1을, 아니면 count를 주어진 문제의 결과로 반환한다.

# 해설
- 각 자리 값을 1과 XOR 비트 연산을 수행하면 1은 0으로, 0은 1로 플립하게 된다.
- 처음부터 연속된 자리의 플립을 수행하는 중, 마지막 두 자리의 값이 0이 아니면 1이 아닌 값이 남게 되므로 절대 모든 값을 1로 만들 수 없다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumOperationsToMakeBinaryArrayElementsEqualToOneI.java){:target="_blank"}에서 확인 가능합니다.