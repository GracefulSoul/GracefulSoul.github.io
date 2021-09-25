---
title: "Leetcode Java Largest Number"
excerpt: "Leetcode Largest Number Java 풀이"
last_modified_at: 2021-09-25T12:00:00
header:
  image: /assets/images/leetcode/largest-number.png
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
[Link](https://leetcode.com/problems/largest-number/){:target="_blank"}

# 코드
```java
class Solution {

  public String largestNumber(int[] nums) {
    String result = Arrays.stream(nums)
        .mapToObj(String::valueOf)
        .sorted((s1, s2) -> (s2 + s1).compareTo(s1 + s2))
        .collect(Collectors.joining(""));
    return result.startsWith("00") ? "0" : result;
  }


}
```

# 결과
[Link](https://leetcode.com/submissions/detail/560507033/){:target="_blank"}

# 설명
1. 양의 정수로만 이루어진 주어진 배열 nums를 이용하여 가장 큰 숫자의 문자형을 만드는 문제이다.

2. 주어진 배열을 Arrays를 활용하여 가장 큰 숫자의 문자형으로 만들어준다.
- stream 메서드를 이용하여 nums를 Stream 객체로 전환한다.
- mapToObj 메서드를 이용하여 int형의 값들을 String으로 변환한다.
- sorted 메서드를 이용하여 내부 값들을 정렬시켜준다.
  - 배열 내 값들을 문자열의 조합으로 더 큰 값이 앞으로 갈 수 있도록 정렬한다.
- collect 메서드를 이용하여 배열을 문자열로 연결시켜준다.

3. 조합된 문자열이 "00"으로 시작될 경우 "0"을, 그 외의 경우 result를 주어진 문제의 결과로 반환한다.
- 조합된 문자열이 "00"인 경우, 0이 가장 큰 값이므로 "00", "000" 등의 값들을 정수인 "0"으로 바꾸어 주는 것이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LargestNumber.java){:target="_blank"}에서 확인 가능합니다.