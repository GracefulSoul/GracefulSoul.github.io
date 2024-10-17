---
title: "Leetcode Java Continuous Subarray Sum"
excerpt: "Leetcode - 'Continuous Subarray Sum' 문제 Java 풀이"
last_modified_at: 2022-06-09T19:00:00
header:
  image: /assets/images/leetcode/continuous-subarray-sum.png
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
[Link](https://leetcode.com/problems/continuous-subarray-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkSubarraySum(int[] nums, int k) {
    int length = nums.length;
    int sum = nums[length - 1];
    for (int i = length - 2; i >= 0; i--) {
      if (nums[i] == 0 && nums[i + 1] == 0) {
        return true;
      } else {
        sum += nums[i];
      }
      if (sum == 0 || sum >= k) {
        int subSum = nums[i];
        for (int j = i + 1; j < length; j++) {
          subSum += nums[j];
          if (subSum % k == 0) {
            return true;
          }
        }
      }
    }
    return false;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/718024868/){:target="_blank"}

# 설명
1. nums의 최소 2개 이상의 연속된 요소로 이루어진 부분 배열의 합이 k의 배수를 충족하는지 검증하는 문제이다.
- 0은 항상 k의 배수이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 num의 길이를 저장한 변수이다.
- sum은 연속된 값의 합을 저장하기 위한 변수로, nums의 $legnth - 1$번째 값을 넣어준다.
  - 부분 배열은 최소 2개 이상의 연속된 요소로 이루어져야 하므로, 모든 sum은 하나의 값을 넣어 초기화하고 다음 위치의 값부터 검증을 수행해야한다.

3. $length - 2$ 부터 0까지 i를 감소시키며 아래의 반복을 수행한다.
- nums의 i번째 값과 $i + 1$번째 값이 0이면 두 값의 합은 0으므로 무조건 k의 배수를 충족하므로, true를 주어진 문제의 결과로 반환한다.
- 그렇지 않은 경우 sum에 nums의 i번째 값을 넣어준다.
- sum이 0이거나 k 이상인 경우 아래를 수행하여 부분 배열의 합이 조건을 만족하는지 검사한다.
  - 부분 배열의 합을 저장하기 위한 subSum을 정의하여 nums[i]을 넣어주고, $i + 1$부터 length까지 j를 증가시키며 subSum에 값을 더해준다.
  - 위의 subSum이 k의 배수를 만족하면, true를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 최소 2개 이상의 연속된 요소로 이루어진 부분 배열의 합이 k의 배수가 되는 경우가 없으므로, false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ContinuousSubarraySum.java){:target="_blank"}에서 확인 가능합니다.