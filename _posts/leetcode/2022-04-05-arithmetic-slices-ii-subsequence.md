---
title: "Leetcode Java Arithmetic Slices II - Subsequence"
excerpt: "Leetcode Arithmetic Slices II - Subsequence Java 풀이"
last_modified_at: 2022-04-05T12:00:00
header:
  image: /assets/images/leetcode/arithmetic-slices-ii-subsequence.png
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
[Link](https://leetcode.com/problems/arithmetic-slices-ii-subsequence/){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfArithmeticSlices(int[] nums) {
    int result = 0;
    int length = nums.length;
    int[][] dp = new int[length][length];
    Map<Long, List<Integer>> map = new HashMap<>();
    for (int i = 0; i < length; i++) {
      for (int j = i + 1; j < length; j++) {
        List<Integer> list = map.get(nums[i] - (nums[j] - (long) nums[i]));
        if (list == null) {
          continue;
        }
        for (int num : list) {
          dp[i][j] += dp[num][i] + 1;
        }
        result += dp[i][j];
      }
      map.computeIfAbsent((long) nums[i], k -> new ArrayList<>()).add(i);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/673997445/){:target="_blank"}

# 설명
1. 정수 배열 nums의 최소 3개 이상의 요소가 포함된 부분 배열이 산술적 수열이 되는 조합의 수를 반환하는 문제이다.
- 각 요소 간 값의 차이가 동일한 값들을 모은 부분 배열은 산술적 수열이다.
- 테스트 케이스는 결과가 32 비트 정수가 되도록 제공된다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 산술적 수열이 되는 조합의 수를 저장하기 위한 변수로, 0으로 초기화한다.
- length는 nums의 길이를 저장할 변수로, nums의 길이로 초기화한다.
- dp는 각 부분 수열의 개수를 계산하기 위한 변수로, $length \times length$ 크기의 2차원 정수 배열로 초기화한다.
- map은 nums 내 각 요소의 위치 값을 저장하기 위한 변수로, HashMap으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 반복하여 아래를 수행한다.
- $i + 1$ 부터 length 미만까지 j를 증가시키며 반복하여 아래를 수행한다.
  - map에서 nums의 j번째 값과 i번째 값의 차이만큼 발생하는 i번째 값 이하 값에 해당하는 List를 가져온다.
  - list가 null인 경우 동일한 차이가 발생하는 값이 존재하지 않으므로, 무시하고 j를 증가시켜 반복을 계속 수행한다.
  - list의 값들을 반복하여 dp[i][j]의 값에 $dp[num][i] + 1$을 계속 더해준다.
  - result에 dp[i][j] 값을 더해 가능한 부분 배열의 수를 증가시킨다.
- map에 nums의 i번째 값이 있는지 확인하여 없으면 새 ArrayList를 넣고, 해당 List에 해당 값의 위치인 i를 넣어준다.

4. 반복이 완료되면 nums 내 3개 이상의 요소를 이용한 부분 배열이 산술적 수열이 되는 개수를 계산한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ArithmeticSlicesIISubsequence.java){:target="_blank"}에서 확인 가능합니다.