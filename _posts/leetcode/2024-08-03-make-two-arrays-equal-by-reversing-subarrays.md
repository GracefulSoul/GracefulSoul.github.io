---
title: "Leetcode Java Make Two Arrays Equal by Reversing Subarrays"
excerpt: "Leetcode Make Two Arrays Equal by Reversing Subarrays Java"
last_modified_at: 2024-08-03T11:20:00
header:
  image: /assets/images/leetcode/make-two-arrays-equal-by-reversing-subarrays.png
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
[Link](https://leetcode.com/problems/make-two-arrays-equal-by-reversing-subarrays/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canBeEqual(int[] target, int[] arr) {
    int[] counts = new int[1001];
    for (int i = 0; i < target.length; i++) {
      counts[target[i]]++;
      counts[arr[i]]--;
    }
    for (int count : counts) {
      if (count != 0) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/make-two-arrays-equal-by-reversing-subarrays/submissions/1342432909/){:target="_blank"}

# 설명
1. arr 배열로 target 배열과 동일한 형태로 만들 수 있는지 검증하는 문제이다.

2. counts는 target과 arr 배열 내 값들의 갯수를 계산하기 위한 변수로, 최댓값인 1000보다 1 큰 크기의 정수 배열로 초기화하고 아래를 수행한다.
- target 배열 내 값에 해당하는 위치의 값을 각각 증가시켜준다.
- arr 배열 내 값에 해당하는 위치의 값을 각각 감소시켜준다.

3. counts 내 모든 값이 0이 아닌 경우, 변환이 불가능하므로 false를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 변환이 가능하므로 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MakeTwoArraysEqualByReversingSubarrays.java){:target="_blank"}에서 확인 가능합니다.