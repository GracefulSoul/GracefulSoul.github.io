---
title: "Leetcode Java Apply Operations to an Array"
excerpt: "Leetcode - 'Apply Operations to an Array' 문제 Java 풀이"
last_modified_at: 2025-03-01T10:00:00
header:
  image: /assets/images/leetcode/apply-operations-to-an-array.png
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
[Link](https://leetcode.com/problems/apply-operations-to-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] applyOperations(int[] nums) {
    int length = nums.length;
    int index = 0;
    for (int i = 0; i < length; i++) {
      if (i < length - 1 && nums[i] == nums[i + 1]) {
        nums[i] *= 2;
        nums[i + 1] = 0;
      }
      if (nums[i] != 0) {
        if (i != index) {
          int temp = nums[i];
          nums[i] = nums[index];
          nums[index] = temp;
        }
        index++;
      }
    }
    return nums;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/apply-operations-to-an-array/submissions/1558653840/){:target="_blank"}

# 설명
1. nums 내 값들을 아래 규칙대로 수행하고 0이 아닌 값을 좌측으로 몰아 반환하는 문제이다.
- nums[i] == nums[i + 1]의 경우, nums[i]의 값은 두 배로 증가시키고 nums[$i + 1$]의 값은 0으로 바꿔준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- index는 0이 아닌 값이 존재하는 위치를 저장할 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- i의 값이 $length - 1$보다 작으면서 nums[i]의 값이 nums[$i + 1$]의 값과 동일하면, nums[i]의 값을 두 배로 증가시키고 nums[$i + 1$]의 위치에 0을 넣어준다.
- nums[i]의 값이 0이 아닌 경우, 아래를 수행한다.
  - i가 index와 다른 경우, nums[i]의 값과 nums[index]의 값을 바꾸어준다.
  - index를 증가시켜 다음 위치로 이동시켜준다.

4. 반복이 완료되어 수정된 배열 nums를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ApplyOperationsToAnArray.java){:target="_blank"}에서 확인 가능합니다.