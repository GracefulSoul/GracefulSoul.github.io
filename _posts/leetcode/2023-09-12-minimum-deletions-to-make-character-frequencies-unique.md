---
title: "Leetcode Java Minimum Deletions to Make Character Frequencies Unique"
excerpt: "Leetcode Minimum Deletions to Make Character Frequencies Unique Java"
last_modified_at: 2023-09-12T18:30:00
header:
  image: /assets/images/leetcode/minimum-deletions-to-make-character-frequencies-unique.png
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
[Link](https://leetcode.com/problems/minimum-deletions-to-make-character-frequencies-unique){:target="_blank"}

# 코드
```java
class Solution {

  public int minDeletions(String s) {
    int[] count = new int[26];
    for (char c : s.toCharArray()) {
      count[c - 'a']++;
    }
    Set<Integer> set = new HashSet<>();
    int result = 0;
    for (int i = 0; i < count.length; i++) {
      int freq = count[i];
      while (freq > 0) {
        if (!set.contains(freq)) {
          set.add(freq);
          break;
        }
        freq--;
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-deletions-to-make-character-frequencies-unique/submissions/1047334213/){:target="_blank"}

# 설명
1. 문자열 s 내 동일한 문자의 갯수가 유일한 문자열이 되기 위해 삭제할 문자의 갯수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 문자열 s의 각 문자의 갯수를 저장할 변수로, 각 문자 별 갯수를 계산하여 넣어준다.
- set은 고유 문자의 갯수를 저장할 변수로, 중복을 제거하기 위해 HashSet으로 초기화한다.
- result는 삭제할 문자의 수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 count의 길이 미만까지 i를 증가시키며 아래를 반복한다.
- freq는 count의 i번째 값을 꺼내 저장한다.
- freq가 0보다 클 때까지 아래를 반복한다.
  - set에서 freq가 존재하지 않는 고유한 수인 경우, set에 freq를 넣고 반복을 중단한다.
  - 위의 경우가 아니라면 freq를 감소시키고 삭제한 수인 result를 증가시킨다.

4. 반복이 완료되면 제거한 문자의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumDeletionsToMakeCharacterFrequenciesUnique.java){:target="_blank"}에서 확인 가능합니다.