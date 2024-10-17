---
title: "Leetcode Java Maximum Number of Balloons"
excerpt: "Leetcode Easy - 'Maximum Number of Balloons' 문제 Java 풀이"
last_modified_at: 2024-09-20T23:30:00
header:
  image: /assets/images/leetcode/maximum-number-of-balloons.png
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
[Link](https://leetcode.com/problems/maximum-number-of-balloons/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxNumberOfBalloons(String text) {
    int[] count = new int[26];
    for (char c : text.toCharArray()) {
      count[c - 'a']++;
    }
    int result = count[1];
    result = Math.min(result, count[0]);
    result = Math.min(result, count[11] / 2);
    result = Math.min(result, count[14] / 2);
    result = Math.min(result, count[13]);
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-number-of-balloons/submissions/1396513929/){:target="_blank"}

# 설명
1. text 문자열 내 문자들을 이용하여 "balloon" 문자열 몇 개를 만들 수 있는지 검증하는 문제이다.

2. count는 text의 문자들을 계산할 변수로, 영문자 갯수인 26 크기의 정수 배열로 초기화하여 text를 처음부터 끝까지 문자 갯수를 계산해 넣어준다.

3. result는 결과를 저장할 변수로, b 문자의 갯수인 count[1]을 넣고 아래 규칙에 따라 만들 수 있는 "balloon" 문자열의 갯수를 주어진 문제의 결과로 반환한다.
- result에 result와 a 문자의 갯수인 count[0] 중 작은 값을 넣어준다.
- result에 result와 l 문자의 갯수인 count[11]를 두 번 들어가므로 2로 나눈 값 중 작은 값을 넣어준다.
- result에 result와 o 문자의 갯수인 count[14]를 두 번 들어가므로 2로 나눈 값 중 작은 값을 넣어준다.
- result에 result와 n 문자의 갯수인 count[0] 중 작은 값을 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumNumberOfBalloons.java){:target="_blank"}에서 확인 가능합니다.