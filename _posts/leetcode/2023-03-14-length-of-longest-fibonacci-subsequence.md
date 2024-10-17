---
title: "Leetcode Java Length of Longest Fibonacci Subsequence"
excerpt: "Leetcode - 'Length of Longest Fibonacci Subsequence' 문제 Java 풀이"
last_modified_at: 2023-03-14T20:00:00
header:
  image: /assets/images/leetcode/length-of-longest-fibonacci-subsequence.png
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
[Link](https://leetcode.com/problems/length-of-longest-fibonacci-subsequence){:target="_blank"}

# 코드
```java
class Solution {

  public int lenLongestFibSubseq(int[] arr) {
    int length = arr.length;
    int[][] dp = new int[length][length];
    int result = 0;
    for (int i = 2; i < length; i++) {
      int left = 0;
      int right = i - 1;
      while (left < right) {
        int val = arr[left] + arr[right] - arr[i];
        if (val < 0) {
          left++;
        } else if (val > 0) {
          right--;
        } else {
          dp[right][i] = dp[left][right] + 1;
          result = Math.max(result, dp[right][i]);
          left++;
          right--;
        }
      }
    }
    return result == 0 ? 0 : result + 2;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/length-of-longest-fibonacci-subsequence/submissions/914948793/){:target="_blank"}

# 설명
1. 최소 3개 이상의 값이 존재하는 arr의 값들을 이용하여 만들 수 있는 피보나치 수열의 최대 길이를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- dp는 만들 수 있는 피보나치 수열의 최대 길이를 저장하기 위한 배열로, $length \times length$ 크기의 배열로 정의한다.
- result는 최대 길이를 저장할 변수로, 0으로 초기화한다.

3. 피보나치 수열의 최소 위치인 2부터 length 미만까지 i를 증가시키며 아래를 반복한다.
- left와 right는 위치 탐색에 필요한 변수로, 0과 $i - 1$로 초기화한다.
- left가 right 미만일 때 까지 아래를 반복한다.
  - val에 arr의 left번째 값과 right번째 값을 더하고, i번째 값을 빼준다.
  - val 값이 0 미만이면 left를 증가시키고 0 초과이면 right를 감소시켜 범위를 좁혀준다.
  - val 값이 0이면 피보나치 수열을 만족하므로, dp[right][i]의 위치에 dp[left][right]의 값보다 1 큰 값으로 넣어준 후 left를 증가시키고 right를 감소시킨다.

4. 반복이 완료되면 result가 0이면 0을, 아니면 피보나치 수열을 만족하는 숫자의 갯수가 존재하므로 2를 더해서 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LengthOfLongestFibonacciSubsequence.java){:target="_blank"}에서 확인 가능합니다.