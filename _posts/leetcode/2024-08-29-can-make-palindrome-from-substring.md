---
title: "Leetcode Java Can Make Palindrome from Substring"
excerpt: "Leetcode Medium - 'Can Make Palindrome from Substring' 문제 Java 풀이"
last_modified_at: 2024-08-29T18:20:00
header:
  image: /assets/images/leetcode/can-make-palindrome-from-substring.png
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
[Link](https://leetcode.com/problems/can-make-palindrome-from-substring/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Boolean> canMakePaliQueries(String s, int[][] queries) {
    int[] counts = new int[s.length() + 1];
    for (int i = 0; i < s.length(); i++) {
      counts[i + 1] = counts[i] ^ (1 << (s.charAt(i) - 'a'));
    }
    List<Boolean> result = new ArrayList<>();
    for (int[] query : queries) {
      result.add(((((query[1] - query[0]) % 2) + Integer.bitCount(counts[query[1] + 1] ^ counts[query[0]])) / 2) <= query[2]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/can-make-palindrome-from-substring/submissions/1372015236/){:target="_blank"}

# 설명
1. 문자열 s가 주어지면 queries를 이용하여 각 조건이 회문 문자열을 만들 수 있는지 검증하는 문제이다.
- queries[i] = [left<sub>i</sub>, right<sub>i</sub>, k<sub>i</sub>]일때, s의 [left<sub>i</sub>, right<sub>i</sub>] 범위 내 문자들을 k<sub>i</sub>개 문자를 변경할 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 문자가 존재하는지 여부를 저장할 변수로, s의 길이보다 1 큰 정수 배열로 초기화하고 s를 순차적으로 반복하여 아래를 수행한다.
  - counts[$i + 1$]에 counts[i]와 1을 현재 문자의 영문자 순서만큼 좌측으로 이동한 비트와 XOR(^) 연산을 수행한 결과를 넣어 홀수번 반복된 문자들을 기준으로 숫자로 넣어준다.
- result는 결과를 순차적으로 넣을 변수로, ArrayList로 초기화한다.

3. queries를 순차적으로 query에 넣어 아래를 수행한다.
- result에 아래의 XOR(^) 연산 결과에 2를 나눈 결과가 query[2]인 변경 가능한 문자 갯수보다 작으면 true를, 아니면 false를 넣어준다.
  - $query[1] - query[0]$을 2로 나눈 나머지 값에 counts의 $query[1] + 1$번째 값의 비트 값이 1인 갯수를 더한 결과.
  - counts의 query[0]번째 값.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 해설
- 비트 값이 1인 홀수 갯수의 문자들 중 절반을 바꾸는 경우, 회문이 가능하다.
- 위의 기준으로 XOR(^) 연산 결과인 홀수개의 문자의 절반이 query[2]인 변경 가능한 문자 갯수보다 큰지 적은지에 따라서 회문 문자열 생성의 여부가 결정된다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CanMakePalindromeFromSubstring.java){:target="_blank"}에서 확인 가능합니다.