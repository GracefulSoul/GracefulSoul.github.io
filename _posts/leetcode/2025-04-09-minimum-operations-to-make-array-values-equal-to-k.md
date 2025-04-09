---
title: "Leetcode Java Minimum Operations to Make Array Values Equal to K"
excerpt: "Leetcode - 'Minimum Operations to Make Array Values Equal to K' 문제 Java 풀이"
last_modified_at: 2025-04-09T18:10:00
header:
  image: /assets/images/leetcode/minimum-operations-to-make-array-values-equal-to-k.png
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
[Link](https://leetcode.com/problems/minimum-operations-to-make-array-values-equal-to-k/){:target="_blank"}

# 코드
```java
class Solution {

  public int minOperations(int[] nums, int k) {
    boolean[] seen = new boolean[101];
    for (int num : nums) {
      seen[num] = true;
    }
    int count = 0;
    for (int i = 1; i < 101; i++) {
      if (seen[i]) {
        if (i < k) {
          return -1;
        } else if (i > k) {
          count++;
        }
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-operations-to-make-array-values-equal-to-k/submissions/1601517781/){:target="_blank"}

# 설명
1. nums의 각 값을 아래의 규칙을 수행하며 모든 값을 k로 만들 수 있는 최소 횟수를 반환하는 문제이다.
- 배열에서 h보다 큰 모든 값이 같은 유효한 값인 h를 선택하여, nums[i] > h를 만족하면 nums[i]의 위치에 h를 넣어준다.
- 모든 값을 k로 만들 수 없는 경우, -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- seen은 nums 내 값을 기록하기 위한 변수로, 값의 범위보다 1 큰 101 크기의 부울 배열로 초기화하고 nums 내 값들의 위치에 true를 넣어준다.
- count는 조건을 만족하는 최소 횟수를 저장할 변수로, 0으로 초기화한다.

3. 1부터 101 미만까지 i를 증가시키며 아래를 반복한다.
- seen[i]가 true인 경우, 아래를 수행한다.
  - i가 k보다 작으면 k로 값을 변경할 수 없으므로, -1을 주어진 문제의 결과로 반환한다.
  - i가 k보다 크면 k로 값을 변경할 수 있으므로, count를 증가시킨다.

4. 반복이 완료되면 계산된 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumOperationsToMakeArrayValuesEqualToK.java){:target="_blank"}에서 확인 가능합니다.