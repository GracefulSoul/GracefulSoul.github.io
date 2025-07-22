---
title: "Leetcode Java Maximum Erasure Value"
excerpt: "Leetcode - 'Maximum Erasure Value' 문제 Java 풀이"
last_modified_at: 2025-07-22T19:40:00
header:
  image: /assets/images/leetcode/maximum-erasure-value.png
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
[Link](https://leetcode.com/problems/maximum-erasure-value/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumUniqueSubarray(int[] nums) {
    int length = nums.length;
    int sum = 0;
    int result = 0;
    int[] index = new int[10001];
    for (int left = 0, right = 0; right < length; right++) {
      while (left < index[nums[right]]) {
        sum -= nums[left++];
      }
      sum += nums[right];
      result = Math.max(sum, result);
      index[nums[right]] = right + 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-erasure-value/submissions/1707115469/){:target="_blank"}

# 설명
1. nums 내 고유한 값으로 이루어진 연속된 순서의 단 하나의 부분 배열을 제거하고 합한 값이 최대인 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- sum은 합계를 저장할 변수로, 0으로 초기화한다.
- result는 최대 합계를 저장할 변수로, 0으로 초기화한다.
- index는 값을 저장할 변수로, 값의 상한선보다 1 큰 $10^4 + 1$ 크기의 정수 배열로 초기화한다.

3. left를 0으로, right가 0부터 length 미만까지 right를 증가시키며 아래를 반복한다.
- left가 index[nums[right]]의 값보다 작을 때 까지, sum에서 nums[left]의 값을 빼고 left를 증가시키는 것을 반복하여 합계에서 부분 범위 내 값들을 빼준다.
- sum에 nums[right]를 추가하여 right번째 값을 포함시켜준다.
- result에 지금까지 합계인 sum과 이전 최대 값인 result 중 큰 값을 넣어준다.
- index[nums[right]]의 위치에 $right + 1$을 넣어 위치 값을 저장한다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumErasureValue.java){:target="_blank"}에서 확인 가능합니다.