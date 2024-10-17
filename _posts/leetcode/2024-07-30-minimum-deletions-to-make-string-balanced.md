---
title: "Leetcode Java Minimum Deletions to Make String Balanced"
excerpt: "Leetcode Medium - 'Minimum Deletions to Make String Balanced' 문제 Java 풀이"
last_modified_at: 2024-07-30T18:00:00
header:
  image: /assets/images/leetcode/minimum-deletions-to-make-string-balanced.png
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
[Link](https://leetcode.com/problems/minimum-deletions-to-make-string-balanced/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimumDeletions(String s) {
    int result = 0;
    int count = 0;
    for (char c : s.toCharArray()) {
      if (c == 'b') {
        count++;
      } else {
        result = Math.min(result + 1, count);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-deletions-to-make-string-balanced/submissions/1338231271/){:target="_blank"}

# 설명
1. s의 문자열을 아래의 조건을 만족하는 문자열로 바꿀 최소 횟수를 계산하는 문제이다.
- i < j 를 만족할 때, s[i] = 'b' 이고 s[j] = 'a' 인 문자열이 없어야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 최소 횟수를 저장할 변수로, 0으로 초기화한다.
- count는 a로 변환할 갯수를 계산할 변수로, 0으로 초기화한다.

3. s의 각 문자들을 처음부터 c에 넣어 아래를 수행한다.
- c가 'b' 문자인 경우, 'a'로 변환하는 횟수인 count를 증가시켜준다.
- c가 'a' 문자인 경우, result에 'b'로 변환하는 경우로 result를 증가시킨 값과 변환시키지 않고 'a'로 변환된 갯수인 count 중 작은 값을 넣어준다.

4. 반복이 완료되면 최소 횟수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumDeletionsToMakeStringBalanced.java){:target="_blank"}에서 확인 가능합니다.