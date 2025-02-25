---
title: "Leetcode Java Number of Sub-arrays With Odd Sum"
excerpt: "Leetcode - 'Number of Sub-arrays With Odd Sum' 문제 Java 풀이"
last_modified_at: 2025-02-25T10:20:00
header:
  image: /assets/images/leetcode/number-of-sub-arrays-with-odd-sum.png
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
[Link](https://leetcode.com/problems/number-of-sub-arrays-with-odd-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public int numOfSubarrays(int[] arr) {
    int result = 0;
    int odd = 0;
    for (int i = 0; i < arr.length; i++) {
      if (arr[i] % 2 == 1) {
        odd = i - odd + 1;
      }
      result = (result + odd) % 1000000007;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-sub-arrays-with-odd-sum/submissions/1554386465/){:target="_blank"}

# 설명
1. arr 내 홀수로 이루어진 값들로 만든 부분 배열의 합이 홀수인 값들의 갯수를 계산하는 문제이다.
- 값이 매우 클 수 있으므로, 모듈러 $10^9 + 7$을 적용한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 결과를 저장할 변수로, 0으로 초기화한다.
- odd는 홀수인 하위 배열의 갯수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 arr 길이 미만까지 i를 증가시키며 아래를 반복한다.
- arr[i]의 값이 홀수인 경우, odd에 $i - odd + 1$인 이전까지 홀수의 부분 배열의 갯수를 증가시켜 넣어 준다.
- result에 $result + odd$에 모듈러 $10^9 + 7$을 적용한 값을 넣어준다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfSubarraysWithOddSum.java){:target="_blank"}에서 확인 가능합니다.