---
title: "Leetcode Java Number of Substrings With Only 1s"
excerpt: "Leetcode - 'Number of Substrings With Only 1s' 문제 Java 풀이"
last_modified_at: 2025-11-16T21:00:00
header:
  image: /assets/images/leetcode/number-of-substrings-with-only-1s.png
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
[Link](https://leetcode.com/problems/number-of-substrings-with-only-1s/){:target="_blank"}

# 코드
```java
class Solution {

  public int numSub(String s) {
    int result = 0;
    int count = 0;
    int mod = 1000000007;
    for (char c : s.toCharArray()) {
      if (c == '1') {
        count++;
        result = (result + count) % mod;
      } else {
        count = 0;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-substrings-with-only-1s/submissions/1831281919/){:target="_blank"}

# 설명
1. 문자열 s의 '1' 문자가 반복된 갯수들의 합을 구하는 문제이다.
- 단, 답이 매우 클 수 있으므로 모듈러 $10^9 + 7$을 이용해 계산한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 문자열 s의 '1' 문자가 반복된 갯수들의 합을 저장할 변수로, 0으로 초기화한다.
- count는 '1' 문자가 반복된 갯수를 계산할 변수로, 0으로 초기화한다.
- mod는 모듈러 $10^9 + 7$를 적용하기 위한 변수이다.

3. s의 문자들을 순차적으로 c에 넣고 아래를 수행한다.
- c가 '1' 문자인 경우, 아래를 수행한다.
  - count를 증가시켜 반복된 '1'의 갯수를 증가시켜준다.
  - result에 모듈러 $10^9 + 7$를 적용한 result와 count의 합계를 넣어준다.
- 그 외인 c가 '0' 문자인 경우, count를 0으로 초기화시켜준다.

4. 반복이 완료되면 계산된 result의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfSubstringsWithOnly1s.java){:target="_blank"}에서 확인 가능합니다.