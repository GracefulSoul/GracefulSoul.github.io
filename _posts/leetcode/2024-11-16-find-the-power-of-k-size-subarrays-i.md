---
title: "Leetcode Java Find the Power of K-Size Subarrays I"
excerpt: "Leetcode - 'Find the Power of K-Size Subarrays I' 문제 Java 풀이"
last_modified_at: 2024-11-16T11:00:00
header:
  image: /assets/images/leetcode/find-the-power-of-k-size-subarrays-i.png
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
[Link](https://leetcode.com/problems/find-the-power-of-k-size-subarrays-i/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] resultsArray(int[] nums, int k) {
    int length = nums.length;
    int[] result = new int[length - k + 1];
    int sum = 0;
    for (int i = 0; i < k - 1; i++) {
      sum += nums[i];
    }
    int index = 0;
    for (int i = 0, j = k - 1; j < length; i++, j++, index++) {
      sum += nums[j];
      if ((k * (nums[i] + nums[i] + k - 1) / 2) == sum && nums[i] <= nums[j]) {
        result[index] = nums[j];
      } else {
        result[index] = -1;
      }
      sum -= nums[i];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-power-of-k-size-subarrays-i/submissions/1453939643/){:target="_blank"}

# 설명
1. nums를 이용하여 연속된 k 개의 요소로 이루어진 부분 배열이 아래의 조건을 만족하는지 여부를 배열로 각각 반환하는 문제이다.
- k개의 요소는 오름차순으로 구성될 때, 최댓값을 넣는다.
- 오름차순이 성립되지 않으면 -1을 넣는다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- result는 결과를 넣을 변수로, k개의 연속된 요소의 부분 배열의 갯수인 $length - k + 1$ 크기의 정수 배열로 초기화한다.
- sum은 k개의 합계를 저장할 변수로, nums의 처음 k개의 값들의 합을 넣어준다.
- index는 result의 위치를 저장항 변수로, 처음 위치인 0으로 초기화한다.

3. i는 0부터, j는 $k - 1$부터 length 미만까지 i, j, index를 증가시키면서 아래를 반복한다.
- sum에 nums[j]의 값을 더해준다.
- 만일 $\frac{k \times (nums[i] + nums[i] + k - 1)}{2} = sum$을 만족하면서 nums[i]의 값이 nums[j] 이하인 증가하는 배열인 경우, result[index]에 가장 큰 nums[j]의 값을 넣어준다.
- 위의 조건을 만족하지 않는 경우, result[index]에 -1을 넣어준다.
- sum에 nums[i]의 값을 빼준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindThePowerOfKSizeSubarraysI.java){:target="_blank"}에서 확인 가능합니다.