---
title: "Leetcode Java K Radius Subarray Averages"
excerpt: "Leetcode K Radius Subarray Averages Java"
last_modified_at: 2023-06-20T19:00:00
header:
  image: /assets/images/leetcode/k-radius-subarray-averages.png
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
[Link](https://leetcode.com/problems/k-radius-subarray-averages){:target="_blank"}

# 코드
```java
class Solution {

  public int[] getAverages(int[] nums, int k) {
    int length = nums.length;
    int size = (2 * k) + 1;
    int[] result = new int[length];
    Arrays.fill(result, -1);
    if (length < size) {
      return result;
    }
    long sum = 0;
    for (int i = 0; i < length; i++) {
      sum += nums[i];
      if (i - size >= 0) {
        sum -= nums[i - size];
      }
      if (i >= size - 1) {
        result[i - k] = (int) (sum / size);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/k-radius-subarray-averages/submissions/975455923/){:target="_blank"}

# 설명
1. nums에서 임의 위치 i의 좌우가 k개로 이루어진 부분 배열 내 값들의 평균을 배열로 만들어 반환하는 문제이다.
- 좌우가 k개가 되지 않는 위치의 값은 -1을 넣는다.
- 평균은 소수점을 절사하여 계산한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- size는 좌우가 k개로 이루어진 부분 배열의 크기를 저장할 변수로, 중심을 기준으로 $(2 \times k) + 1$로 초기화한다.
- result는 각 위치 별 부분 배열의 평균을 저장할 변수로, length 길이로 초기화하고 모든 값을 -1로 넣어준다.

3. length가 size보다 작은 경우, 구성할 수 있는 경우가 없으므로 result를 주어진 문제의 결과로 반환한다.

4. sum은 부분 배열의 합계를 저장할 변수로, 0으로 초기화한다.

5. 0부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- sum에 nums의 i번째 값을 넣어주고, $i - size$가 0보다 큰 경우, sum에 부분 배열 범위를 벗어나는 값인 nums의 $i - size$번째 값을 빼준다.
- i가 $size - 1$보다 크거나 같은 경우, 조건을 만족하므로 result의 $i - k$번째 위치에 $\frac{sum}{size}$의 값을 정수로 변환하여 넣어준다.

6. 반복이 완료되면 조건에 맞는 평균 값이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KRadiusSubarrayAverages.java){:target="_blank"}에서 확인 가능합니다.