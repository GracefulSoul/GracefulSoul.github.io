---
title: "Leetcode Java Longest Arithmetic Subsequence of Given Difference"
excerpt: "Leetcode - 'Longest Arithmetic Subsequence of Given Difference' 문제 Java 풀이"
last_modified_at: 2024-12-19T19:30:00
header:
  image: /assets/images/leetcode/longest-arithmetic-subsequence-of-given-difference.png
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
[Link](https://leetcode.com/problems/longest-arithmetic-subsequence-of-given-difference/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestSubsequence(int[] arr, int difference) {
    int[] map = new int[40001];
    int result = 1;
    for (int num : arr) {
      int index = 20000 + num;
      map[index] = map[index - difference] + 1;
      result = Math.max(result, map[index]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-arithmetic-subsequence-of-given-difference/submissions/1482812273/){:target="_blank"}

# 설명
1. arr의 값들을 이용하여 부분 배열의 각 값의 차이가 difference씩인 최대 부분 배열의 길이를 구하는 문제이다.
- 부분 배열은 임의 요소들을 제거하여 구성할 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 arr의 순차적인 값의 차이가 difference인 위치의 값을 저장할 변수로, 값의 최대 갯수인 $2 * 10^4$에서 difference 또한 동일 범위 내 값이 가능하므로 다시 두 배를 한 크기보다 1 큰 $4 * 10^4 + 1$ 크기의 정수 배열로 초기화한다.
- result는 부분 배열의 갯수를 저장할 변수로, 최소 갯수인 1로 초기화한다.

3. arr의 값들을 순차적으로 num에 넣어 아래를 수행한다.
- index은 위치 값을 저장할 변수로, map의 중앙 값인 20000에 num을 더한 값을 넣어준다.
- map[index]에 이전 difference 위치의 값인 map[$index - difference$] 값에 1을 더해 넣어준다.
- result에 이전까지 최대 길이인 result와 현재까지 최대 길이인 map[index] 중 큰 값을 넣어준다.

4. 반복이 완료되면 부분 배열의 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestArithmeticSubsequenceOfGivenDifference.java){:target="_blank"}에서 확인 가능합니다.