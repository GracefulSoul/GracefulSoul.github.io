---
title: "Leetcode Java Maximum Absolute Sum of Any Subarray"
excerpt: "Leetcode - 'Maximum Absolute Sum of Any Subarray' 문제 Java 풀이"
last_modified_at: 2025-02-26T10:10:00
header:
  image: /assets/images/leetcode/maximum-absolute-sum-of-any-subarray.png
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
[Link](https://leetcode.com/problems/maximum-absolute-sum-of-any-subarray/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxAbsoluteSum(int[] nums) {
    int sum = 0;
    int max = 0;
    int min = 0;
    for (int num : nums) {
      sum += num;
      max = Math.max(max, sum);
      min = Math.min(min, sum);
    }
    return max - min;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-absolute-sum-of-any-subarray/submissions/1555526317/){:target="_blank"}

# 설명
1. nums 내 부분 배열 중 값들의 합에 대한 절댓값이 가장 큰 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sum은 합계를 저장할 변수로, 0으로 초기화한다.
- max와 min은 최댓값과 최솟값을 저장할 변수로, 둘 다 0으로 초기화한다.

3. nums의 값들을 순차적으로 num에 넣어 아래를 수행한다.
- sum에 num을 더해준다.
- max와 min에 sum과 자기 자신 중 최댓값과 최솟값을 넣어준다.

4. 반복이 완료되면 $max - min$을 통해 부분 배열의 합이 가장 큰 값과 가장 작은 값의 차잇값을 주어진 문제의 결과로 반환한다.

# 해설
- 배열의 시작부터 합이 가장 크고 작은 위치는 값의 차이에 대한 폭이 가장 크므로, 그 값을 먼저 찾는다.
- 위 두 지점 중 시작부터 가까운 지점까지의 부분 배열을 제외하고, 그 다음 값부터 다음 지점까지 부분 배열이 원하는 조건인 값들의 합에 대한 절댓값이 가장 큰 값이된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumAbsoluteSumOfAnySubarray.java){:target="_blank"}에서 확인 가능합니다.