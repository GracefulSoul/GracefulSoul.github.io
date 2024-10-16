---
title: "Leetcode Java Repeated DNA Sequences"
excerpt: "Leetcode Repeated DNA Sequences Java 풀이"
last_modified_at: 2021-09-27T12:00:00
header:
  image: /assets/images/leetcode/repeated-dna-sequences.png
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
[Link](https://leetcode.com/problems/repeated-dna-sequences/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> findRepeatedDnaSequences(String s) {
    Set<String> result = new HashSet<>();
    Set<String> temp = new HashSet<>();
    for (int idx = 0; idx + 9 < s.length(); idx++) {
      String sequence = s.substring(idx, idx + 10);
      if (!temp.add(sequence)) {
        result.add(sequence);
      }
    }
    return new ArrayList<>(result);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/561619480/){:target="_blank"}

# 설명
1. 주어진 DNA 서열인 s에서 두 번 이상 존재하는 10글자의 DNA 서열을 모두 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 두 번 이상 존재하는 10글자의 DNA 서열을 저장하는 변수이다.
- temp는 두 번 이상 존재하는지 DNA 서열을 모두 저장하기 위한 변수이다.

3. 주어진 문자열을 처음부터 마지막 10자리가 되는 $s.length() - 10$번째 까지 반복하여 두 번 이상 존재하는 10자리의 DNA 서열을 모두 찾는다.
- sequence에 idx부터 10자리의 DNA 서열을 저장한다.
- temp에 sequence를 넣어주고, 이미 들어가 있을 경우 result에도 넣어준다.

4. 반복이 종료되면 전체 DNA 서열인 s에서 두 번 이상 존재하는 DNA 서열이 저장된 result를 ArrayList로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RepeatedDNASequences.java){:target="_blank"}에서 확인 가능합니다.