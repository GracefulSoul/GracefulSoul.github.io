---
title: "Leetcode Java Wiggle Subsequence"
excerpt: "Leetcode - 'Wiggle Subsequence' 문제 Java 풀이"
last_modified_at: 2022-02-05T12:00:00
header:
  image: /assets/images/leetcode/wiggle-subsequence.png
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
[Link](https://leetcode.com/problems/wiggle-subsequence/){:target="_blank"}

# 코드
```java
class Solution {

  public int wiggleMaxLength(int[] nums) {
    int up = 1;
    int down = 1;
    for (int idx = 1; idx < nums.length; idx++) {
      if (nums[idx] > nums[idx - 1]) {
        up = down + 1;
      } else if (nums[idx] < nums[idx - 1]) {
        down = up + 1;
      }
    }
    return Math.max(up, down);
  }


}
```

# 결과
[Link](https://leetcode.com/submissions/detail/634693779/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums의 값들이 파동과 같이 높은 값 -> 낮은 값 -> 높은 값 형태로 구성된 최대 길이를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- up은 현재의 값이 이전의 값보다 커지는 경우 증가시키기 위한 변수로, 1로 초기화한다.
- down은 현재의 값이 이전의 값보다 작아지는 경우 증가시키기 위한 변수로, 1로 초기화한다.

3. nums를 두 번째 값부터 끝까지 탐색하여 up과 down에 횟수를 증가시킨다.
- up의 경우, 이전의 값과 비교하기 때문에 첫 값부터 탐색하는 것이 아니라 두 번째 값부터 탐색한다.
- nums의 idx번째 값이 nums의 $idx - 1$번째 값보다 큰 경우, up에 $down + 1$을 넣어준다.
- nums의 idx번째 값이 nums의 $idx - 1$번째 값보다 작은 경우, down에 $up + 1$을 넣어준다.
- up과 down에 반대 값의 1을 더한 값을 넣은 이유는, 점층적으로 증가 혹은 감소하는 값들의 횟수를 배제하기 위함이다.

4. 반복이 완료되면 up과 down 중 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WiggleSubsequence.java){:target="_blank"}에서 확인 가능합니다.