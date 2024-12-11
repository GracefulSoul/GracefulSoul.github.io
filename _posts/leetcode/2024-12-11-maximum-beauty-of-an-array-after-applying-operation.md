---
title: "Leetcode Java Maximum Beauty of an Array After Applying Operation"
excerpt: "Leetcode - 'Maximum Beauty of an Array After Applying Operation' 문제 Java 풀이"
last_modified_at: 2024-12-11T21:20:00
header:
  image: /assets/images/leetcode/maximum-beauty-of-an-array-after-applying-operation.png
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
[Link](https://leetcode.com/problems/maximum-beauty-of-an-array-after-applying-operation/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumBeauty(int[] nums, int k) {
    Arrays.sort(nums);
    int start = 0;
    int end = 0;
    while (end < nums.length) {
      if (nums[end++] - nums[start] > k * 2) {
        start++;
      }
    }
    return end - start;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-beauty-of-an-array-after-applying-operation/submissions/1476107237/){:target="_blank"}

# 설명
1. nums로 아래 규칙을 이용하여 만들어진 배열 내 제거 혹은 그대로 유지했을 때 동일한 값들로 구성된 부분 배열의 가장 긴 길이를 구하는 문제이다.
- 임의 i번째 값인 nums[i]를 [$nums[i] - k$, $nums[i] + k$] 범위 내 값으로 한 번 변경이 가능하다.

2. nums의 값들을 오름차순 정렬해준다.

3. start와 end는 nums 내 시작과 종료 위치를 저장할 변수로, 둘 다 0으로 초기화한다.

4. end가 nums의 길이 미만일 때 까지 아래를 반복한다.
- nums[end] - nums[start]의 값이 $k \times 2$보다 큰 변환 가능한 범위 밖인 경우, start를 증가시켜 범위를 좁혀준다.

5. 반복이 완료되면 $end - start$인 가장 긴 길이를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumBeautyOfAnArrayAfterApplyingOperation.java){:target="_blank"}에서 확인 가능합니다.