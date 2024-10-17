---
title: "Leetcode Java Minimum Difference Between Largest and Smallest Value in Three Moves"
excerpt: "Leetcode Medium - 'Minimum Difference Between Largest and Smallest Value in Three Moves' 문제 Java 풀이"
last_modified_at: 2024-07-03T18:10:00
header:
  image: /assets/images/leetcode/minimum-difference-between-largest-and-smallest-value-in-three-moves.png
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
[Link](https://leetcode.com/problems/minimum-difference-between-largest-and-smallest-value-in-three-moves/){:target="_blank"}

# 코드
```java
class Solution {

  public int minDifference(int[] nums) {
    int length = nums.length;
    if (length < 5) {
      return 0;
    } else {
      int result = Integer.MAX_VALUE;
      Arrays.sort(nums);
      for (int i = 0; i < 4; i++) {
        result = Math.min(result, nums[length - 4 + i] - nums[i]);
      }
      return result;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-difference-between-largest-and-smallest-value-in-three-moves/submissions/1308038488/){:target="_blank"}

# 설명
1. nums 내 임의 값을 배열 내 값으로 세 번까지 변경하여 최댓값과 최솟값의 차이가 최소가 되는 값을 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 결과를 저장한 변수로 5 미만이면 최댓값과 최솟값이 항상 0이 되므로, 0을 주어진 문제의 결과로 반환한다.
- result는 결과를 저장할 변수로, 정수의 최댓값을 넣어 초기화한다.

3. nums의 값들을 오름차순 정렬 후 0부터 4 미만까지 i를 증가시키며 아래를 반복한다.
- result에 result와 nums의 마지막 위치인 $length - 1$에서 $i - 3$번째 값에 nums[i]를 뺀 최댓값과 최솟값이 가능한 경우의 차잇값 중 작은 값을 넣어준다.

4. 반복이 완료되면 최소 차잇값인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumDifferenceBetweenLargestAndSmallestValueInThreeMoves.java){:target="_blank"}에서 확인 가능합니다.