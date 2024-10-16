---
title: "Leetcode Java Reorganize String"
excerpt: "Leetcode Reorganize String Java"
last_modified_at: 2022-12-17T12:50:00
header:
  image: /assets/images/leetcode/reorganize-string.png
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
[Link](https://leetcode.com/problems/reorganize-string){:target="_blank"}

# 코드
```java
class Solution {

  public String reorganizeString(String s) {
    int length = s.length();
    int[] hash = new int[26];
    for (char c : s.toCharArray()) {
      hash[c - 'a']++;
    }
    int letter = 0;
    int count = 0;
    for (int idx = 0; idx < hash.length; idx++) {
      if (hash[idx] > count) {
        letter = idx;
        count = hash[idx];
      }
    }
    if (count > (length + 1) / 2) {
      return "";
    }
    char[] result = new char[length];
    int index = 0;
    while (hash[letter] > 0) {
      result[index] = (char) (letter + 'a');
      index += 2;
      hash[letter]--;
    }
    for (int idx = 0; idx < hash.length; idx++) {
      while (hash[idx] > 0) {
        if (index >= length) {
          index = 1;
        }
        result[index] = (char) (idx + 'a');
        index += 2;
        hash[idx]--;
      }
    }
    return String.valueOf(result);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/reorganize-string/submissions/860931635/){:target="_blank"}

# 설명
1. s의 문자들이 동일한 문자가 붙지 않도록 재 정렬해서 반환하는 문제이다.
- 동일한 문자가 붙을 수 밖에 없는 경우, 빈 문자열인 ""을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 s의 길이를 저장한 변수이다.
- counts는 s의 각 문자 별 발생 횟수를 저장할 변수로, s의 각 문자를 반복하여 개수를 계산해준다.
- letter와 count는 가장 많이 발생한 문자의 위치와 개수를 저장할 변수로, counts를 반복하여 가장 많이 발생한 문자의 위치와 개수를 저장해준다.
  - count가 length의 절반 이상인 경우, 동일한 문자가 반드시 붙으므로 ""을 주어진 문제의 결과로 반환한다.
- result는 결과 문자열을 만들기 위한 배열로, length 길이의 문자 배열로 초기화한다.
- index는 result에 문자를 순차적으로 넣기 위한 위치 변수로, 0으로 초기화한다.

3. counts의 letter 문자의 개수가 0 초과일 때까지 아래를 반복한다.
- result의 index번째 위치에 letter를 영문자로 변환하여 넣어준다.
- index를 2씩 증가시켜 같은 문자가 붙지 않도록 띄어 넣어준다.
- letter번째 영문자를 사용했으므로, counts 내 개수를 차감해준다.

4. 0부터 counts의 길이까지 idx를 증가시키며 아래를 반복하여 문자열을 완성한다.
- counts의 idx번째 문자의 개수가 0 초과일 때 까지 아래를 반복한다.
  - index가 result의 길이를 초과하는 경우, 이미 들어간 문자 사이에 넣도록 index를 1로 초기화해준다.
  - result의 index번째 위치에 idx를 영문자로 변환하여 넣어준다.
  - index를 2씩 증가시켜 같은 문자가 붙지 않도록 띄어 넣어준다.
  - idx번째 영문자를 사용했으므로, counts 내 개수를 차감해준다.

5. 반복이 완료되면 result를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ReorganizeString.java){:target="_blank"}에서 확인 가능합니다.