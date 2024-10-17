---
title: "Leetcode Java Count Number of Homogenous Substrings"
excerpt: "Leetcode Medium - 'Count Number of Homogenous Substrings' 문제 Java 풀이"
last_modified_at: 2023-11-09T18:40:00
header:
  image: /assets/images/leetcode/count-number-of-homogenous-substrings.png
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
[Link](https://leetcode.com/problems/count-number-of-homogenous-substrings){:target="_blank"}

# 코드
```java
class Solution {

  public int countHomogenous(String s) {
    int count = 0;
    int result = 0;
    char[] charArray = s.toCharArray();
    for (int left = 0, right = 0; right < charArray.length; right++) {
      if (charArray[left] == charArray[right]) {
        count++;
      } else {
        left = right;
        count = 1;
      }
      result = (result + count) % 1000000007;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-number-of-homogenous-substrings/submissions/1095109101/){:target="_blank"}

# 설명
1. s의 연속된 문자열 중 동일한 문자로 이루어진 부분 문자열의 수를 구하는 문제이다.
- "abbaa"의 경우, 아래와 같다.
  - "a"가 3번, "aa"가 1번
  - "b"가 2번, "bb"가 1번
  - 총 7개이다.
- 배열의 크기가 매우 클 수 있으므로 모듈러 $10^9 + 7$을 적용한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 동일한 문자로 이루어진 문자열의 갯수를 저장할 변수로, 0으로 초기화한다.
- result는 부분 문자열의 수를 저장할 변수로, 0으로 초기화한다.
- charArray는 s를 문자 배열로 저장한 변수이다.

3. left와 right가 0부터 right가 charArray 길이 미만일 때 까지 right를 증가시키며 아래를 반복한다.
- charArray의 left번째 문자와 right번째 문자가 동일한 경우, count를 증가시킨다.
- 동일하지 않은 경우, left에 right를 넣어주고 count를 1로 초기화한다.
- result에 result와 count를 더한 후 모듈러 $10^9 + 7$을 적용한 값을 넣어준다.

4. 반복이 완료되면 동일한 문자로 이루어진 부분 문자열의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountNumberOfHomogenousSubstrings.java){:target="_blank"}에서 확인 가능합니다.