---
title: "Leetcode Java K-Concatenation Maximum Sum"
excerpt: "Leetcode K-Concatenation Maximum Sum Java"
last_modified_at: 2024-09-21T10:00:00
header:
  image: /assets/images/leetcode/k-concatenation-maximum-sum.png
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
[Link](https://leetcode.com/problems/k-concatenation-maximum-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public int kConcatenationMaxSum(int[] arr, int k) {
    long currentMax = arr[0] > 0 ? arr[0] : 0L;
    long max = currentMax;
    long sum = arr[0];
    int length = arr.length;
    for (int i = 1; i < Math.min(k, 2) * length; i++) {
      currentMax = Math.max(currentMax + arr[i % length], arr[i % length]);
      max = Math.max(currentMax, max);
      if (i < length) {
        sum += arr[i];
      }
    }
    while (sum > 0 && --k >= 2) {
      max = (max + sum) % 1000000007;
    }
    return (int) max % 1000000007;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/k-concatenation-maximum-sum/submissions/1396950798/){:target="_blank"}

# 설명
1. arr의 값이 k번 이어진 배열에서 부분 배열의 합이 최대인 값을 구하는 문제이다.
- 부분 배열의 값이 없는 경우, 합은 0이다.
- 부분 배열의 합이 매우 클 수 있으므로, 모듈러 $10^9 + 7$을 적용한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- currentMax와 max는 [Kadane's algorithm](https://en.wikipedia.org/wiki/Maximum_subarray_problem#Kadane's_algorithm){:target="_blank"}방식으로 문제 풀이를 하기 위한 변수로, 첫 값이 0보다 크면 해당 값을 아니면 빈 부분 배열의 합인 0을 넣어준다.
- sum은 arr의 값을 더해줄 변수로, arr[0]의 값을 넣어준다.

3. 1부터 k가 2보다 크면 $2 \times k$, 아니면 length까지 i를 증가시키며 아래를 반복한다.
- currentMax에 아래 중 큰 값을 넣어준다.
  - currentMax에 arr의 $\frac{i}{length}$ 값의 몫 위치 값을 더한 값인 현재값까지 최대 합.
  - arr의 $\frac{i}{length}$ 값의 몫 위치 값.
- max에 두 값 중 큰 값을 넣어준다.
  - 이전까지 최대 값인 max.
  - 현재까지 최대 값인 currentMax.
- i가 length 미만인 경우, sum에 arr[i] 값을 누계해준다.

4. 반복이 완료되면 sum이 0보다 크면서 k를 감소한 값이 2보다 클 때 까지, max에 $max + sum$에 모듈러 $10^9 + 7$를 적용한 값을 넣어준다.

5. 최종 결과가 저장된 max애 모듈러 $10^9 + 7$를 적용한 값을 반환 목표인 int형으로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KConcatenationMaximumSum.java){:target="_blank"}에서 확인 가능합니다.