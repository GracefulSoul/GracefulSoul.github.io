---
title: "Leetcode Java Reduction Operations to Make the Array Elements Equal"
excerpt: "Leetcode Medium - 'Reduction Operations to Make the Array Elements Equal' 문제 Java 풀이"
last_modified_at: 2023-11-19T13:10:00
header:
  image: /assets/images/leetcode/reduction-operations-to-make-the-array-elements-equal.png
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
[Link](https://leetcode.com/problems/reduction-operations-to-make-the-array-elements-equal){:target="_blank"}

# 코드
```java
class Solution {

  public int reductionOperations(int[] nums) {
    Arrays.sort(nums);
    int result = 0;
    int length = nums.length;
    for (int i = length - 1; i > 0; i--) {
      if (nums[i - 1] != nums[i]) {
        result += length - i;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reduction-operations-to-make-the-array-elements-equal/submissions/1101858339/){:target="_blank"}

# 설명
1. nums의 값을 내부 값으로 낮춰가면서 모든 값이 동일할 때 까지 걸리는 횟수를 구하는 문제이다.

2. nums의 값들을 오름차순으로 정렬한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- result는 횟수를 계산하기 위한 변수로, 0으로 초기화한다.
- length는 nums의 길이를 저장한 변수이다.

4. $length - 1$부터 0 초과일 때 까지 i를 감소시키면서 아래를 반복한다.
- nums[$i - 1$]의 값과 nums[i]의 값이 다른 경우, result에 바꾸기 위한 횟수인 $length - i$을 더해준다.

5. 반복이 완료되면 감소 횟수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReductionOperationsToMakeTheArrayElementsEqual.java){:target="_blank"}에서 확인 가능합니다.