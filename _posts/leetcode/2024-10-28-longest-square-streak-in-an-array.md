---
title: "Leetcode Java Longest Square Streak in an Array"
excerpt: "Leetcode - 'Longest Square Streak in an Array' 문제 Java 풀이"
last_modified_at: 2024-10-28T18:20:00
header:
  image: /assets/images/leetcode/count-square-submatrices-with-all-ones.png
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
[Link](https://leetcode.com/problems/longest-square-streak-in-an-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int longestSquareStreak(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    Arrays.sort(nums);
    int result = -1;
    for (int num : nums) {
      int sqrt = (int) Math.sqrt(num);
      if (sqrt * sqrt == num && map.containsKey(sqrt)) {
        map.put(num, map.get(sqrt) + 1);
        result = Math.max(result, map.get(num));
      } else {
        map.put(num, 1);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/longest-square-streak-in-an-array/submissions/1436045278/){:target="_blank"}

# 설명
1. 아래의 조건을 만족하는 가장 긴 정수 배열의 길이를 반환하는 문제이다.
- 정수 배열은 최소 2개 이상의 요소를 가진 배열이어야 한다.
- 값을 오름차순으로 정렬하였을 때, 이전 값의 제곱 값이 다음 값으로 존재한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 각 값을 넣어 저장할 변수로, HashMap으로 초기화한다.
- result는 가장 긴 정수 배열의 길이를 저장할 변수로, -1로 초기화한다.

3. nums를 오름차순 정렬하고 num에 순차적으로 넣어 아래를 수행한다.
- sqrt는 num을 제곱근한 값을 저장한 변수이다.
- sqrt의 제곱 값이 nu과 동일하고 map에 sqrt의 값이 존재하면 map의 해당 값에 해당하는 값을 증가시키고, result에 result와 map의 num이 키인 값 중 큰 값인 최대 길이를 넣어준다.
- 위의 경우가 아니라면 map의 num이 키인 값에 1을 넣어준다.

4. 반복이 완료되면 최대 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LongestSquareStreakInAnArray.java){:target="_blank"}에서 확인 가능합니다.