---
title: "Leetcode Java Minimum Length of String After Operations"
excerpt: "Leetcode - 'Minimum Length of String After Operations' 문제 Java 풀이"
last_modified_at: 2025-01-13T18:10:00
header:
  image: /assets/images/leetcode/minimum-length-of-string-after-operations.png
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
[Link](https://leetcode.com/problems/minimum-length-of-string-after-operations/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumLength(String s) {
    int[] counts = new int[26];
    for (char c : s.toCharArray()) {
      counts[c - 'a']++;
    }
    int result = 0;
    for (int count : counts) {
      if (count > 0) {
        if (count % 2 == 0) {
          result += 2;
        } else {
          result++;
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-length-of-string-after-operations/submissions/1507077709/){:target="_blank"}

# 설명
1. 아래의 규칙대로 수행하고 마지막 남은 문자열의 최소 길이를 반환하는 문제이다.
- 좌우에 동일한 문자가 존재하는 임의 문자를 선택하여 앞의 좌우 두 문자를 제거한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 문자열 s의 각 문자 갯수를 계산해서 저장할 변수로, 영문자 갯수인 26 크기의 정수 배열로 초기화하고 s의 각 문자 갯수를 계산해준다.
- result는 남은 문자열의 길이를 계산할 변수로, 0으로 초기화한다.

3. counts의 값들을 순차적으로 count에 넣어 아래를 수행한다.
- count가 0 초과인 s에 존재하는 문자인 경우, 아래를 수행한다.
  - count가 짝수이면 좌우에 값이 존재하므로 result를 2증가시키고, 홀수이면 result를 1증가시킨다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumLengthOfStringAfterOperations.java){:target="_blank"}에서 확인 가능합니다.