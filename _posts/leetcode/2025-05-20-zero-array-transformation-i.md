---
title: "Leetcode Java Zero Array Transformation I"
excerpt: "Leetcode - 'Zero Array Transformation I' 문제 Java 풀이"
last_modified_at: 2025-05-20T18:30:00
header:
  image: /assets/images/leetcode/zero-array-transformation-i.png
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
[Link](https://leetcode.com/problems/zero-array-transformation-i/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isZeroArray(int[] nums, int[][] queries) {
    int length = nums.length;
    int[] counts = new int[length];
    for (int[] query : queries) {
      counts[query[0]]++;
      if (query[1] + 1 < length) {
        counts[query[1] + 1]--;
      }
    }
    int curr = 0;
    for (int i = 0; i < length; i++) {
      curr += counts[i];
      if (curr < nums[i]) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/zero-array-transformation-i/submissions/1639142680/){:target="_blank"}

# 설명
1. nums 내 값을 queries의 구간에 대해서 1씩 줄일 때, 모든 값을 0으로 변환 가능한지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이을 저장한 변수이다.
- counts는 각 값을 계산하기 위한 변수로, length 길이의 정수 배열로 정의하고 queries의 각 값을 순차적으로 query에 넣어 아래를 반복한다.
  - counts 내 query[0] 번째 값을 증가시키고, $query[1] + 1$ 값이 length 미만인 counts 내 해당 값에 대한 값을 감소시킬 수 있으면 감소시킨다.
- curr은 nums 내 음수로 전환되는 값의 갯수를 계산할 변수로, 0으로 초기화한다.

4. 0부터 length까지 i를 증가시키며 아래를 반복한다.
- curr에 counts[i]를 증가시킨 후 curr이 nums[i]보다 작은 0 미만으로 내려가는 경우, false를 주어진 문제의 결과로 반환한다.

5. 반복이 완료되면 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ZeroArrayTransformationI.java){:target="_blank"}에서 확인 가능합니다.