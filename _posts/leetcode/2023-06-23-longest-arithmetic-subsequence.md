---
title: "Leetcode Java Longest Arithmetic Subsequence"
excerpt: "Leetcode Longest Arithmetic Subsequence Java"
last_modified_at: 2023-06-23T19:05:00
header:
  image: /assets/images/leetcode/longest-arithmetic-subsequence.png
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
[Link](https://leetcode.com/problems/longest-arithmetic-subsequence){:target="_blank"}

# 코드
```java
class Solution {

  public int longestArithSeqLength(int[] nums) {
    int result = 0;
    int max = Integer.MIN_VALUE;
    int min = Integer.MAX_VALUE;
    for (int num : nums) {
      max = Math.max(max, num);
      min = Math.min(min, num);
    }
    for (int i = 0; i <= max - min; i++) {
      if (i * result > max - min) {
        break;
      }
      int[] first = new int[501];
      int[] second = new int[501];
      for (int num : nums) {
        first[num] = (num + i <= 500) ? (first[num + i] + 1) : 1;
        second[num] = (num - i >= 0) ? (second[num - i] + 1) : 1;
        result = Math.max(result, Math.max(first[num], second[num]));
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-arithmetic-subsequence/submissions/977758689/){:target="_blank"}

# 설명
1. nums 배열 내 순서 변경 없이, 임의 숫자를 제외하면서 동일한 값의 변화가 이루어지는 최대 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최대 길이를 저장할 변수로, 0으로 초기화한다.
- max와 min은 nums에서 최댓값과 최솟값을 저장할 변수로, nums를 반복하여 최댓값과 최솟값을 넣어준다.

3. 0부터 $max - min$까지 i를 감소시키며 아래를 반복한다.
- $i \times result$의 값이 $max - min$의 값보다 큰 경우, 값의 범위를 벗어나므로 다음 반복을 수행한다.
- first와 second는 값의 차이를 순차적으로 저장할 변수로, nums 내 값의 최댓값인 500보다 1 큰 크기의 정수 배열로 초기화한다.
- nums의 모든 값을 num에 순차적으로 넣고 아래를 반복한다.
  - first의 num번째 위치에 $num + i$가 500보다 같거나 작으면 first의 $num + i$번째 값에 1을 더해서, 아니면 1을 넣어준다.
  - second의 num번째 위치에 $num - i$가 0보다 같거나 크면 second의 $num - i$번째 값에 1을 더해서, 아니면 1을 넣어준다.
  - result에 result와 first와 seconde의 num번쨰 위치의 값들 중 큰 값을 넣어준다.

4. 반복이 완료되면 최대 길이를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestArithmeticSubsequence.java){:target="_blank"}에서 확인 가능합니다.