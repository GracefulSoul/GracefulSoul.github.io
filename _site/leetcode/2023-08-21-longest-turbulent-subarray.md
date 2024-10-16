---
title: "Leetcode Java Longest Turbulent Subarray"
excerpt: "Leetcode Longest Turbulent Subarray Java"
last_modified_at: 2023-08-21T19:00:00
header:
  image: /assets/images/leetcode/longest-turbulent-subarray.png
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
[Link](https://leetcode.com/problems/longest-turbulent-subarray){:target="_blank"}

# 코드
```java
class Solution {

  public int maxTurbulenceSize(int[] arr) {
    int result = 0;
    for (int i = 0, count = 0; i < arr.length - 1; i++, count *= -1) {
      if (arr[i] > arr[i + 1]) {
        count = count > 0 ? count + 1 : 1;
      } else if (arr[i] < arr[i + 1]) {
        count = count < 0 ? count - 1 : -1;
      } else {
        count = 0;
      }
      result = Math.max(result, Math.abs(count));
    }
    return result + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-turbulent-subarray/submissions/1027498967/){:target="_blank"}

# 설명
1. arr 내 이어진 값이 높았다가 낮아지는 구간의 길이를 구하는 문제이다.

2. result는 길이를 저장할 변수로, 0으로 초기화한다.

3. count는 0으로, 0부터 $arr.length - 1$ 미만까지 i를 증가시키고 count에 -1을 곱해주면서 아래를 반복한다.
- arr[i]의 값이 arr[$i + 1$]의 값보다 큰 경우, count가 0보다 크면 1을 증가시키고 아니면 count를 1로 초기화한다.
- 위의 경우가 아니면서 arr[i]의 값이 arr[$i + 1$]보다 작은 경우, count가 0보다 작으면 count를 감소시키고 아니면 -1로 초기화한다.
- 그 외인 두 값이 같으면 count를 0으로 초기화한다.
- result에 result와 count의 절댓값 중 큰 값을 저장한다.

4. 반복이 완료되면 자기 자신을 포함한 $result + 1$을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestTurbulentSubarray.java){:target="_blank"}에서 확인 가능합니다.