---
title: "Leetcode Java Find Common Characters"
excerpt: "Leetcode Find Common Characters Java"
last_modified_at: 2023-10-14T14:30:00
header:
  image: /assets/images/leetcode/find-common-characters.png
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
[Link](https://leetcode.com/problems/find-common-characters){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> commonChars(String[] words) {
    int length = words.length;
    int[][] count = new int[length][26];
    for (int i = 0; i < length; i++) {
      for (int j = 0; j < words[i].length(); j++) {
        count[i][words[i].charAt(j) - 'a']++;
      }
    }
    List<String> result = new ArrayList<>();
    for (int j = 0; j < 26; j++) {
      int min = 101;
      for (int i = 0; i < length; i++) {
        min = Math.min(min, count[i][j]);
      }
      while (min-- > 0) {
        result.add(String.valueOf((char) (j + 'a')));
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/find-common-characters/submissions/1074734484/){:target="_blank"}

# 설명
1. words 문자열 내 공통된 문자들을 추려내는 문제이다.
- 단, 반복된 문자열이 동일한 갯수로 존재하면 동일한 갯수로 넣어준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 words의 길이를 저장한 변수이다.
- count는 각 문자 별 문자의 수를 저장할 변수로, $length \times 26$ 크기의 정수 배열로 초기화하고 각 문자를 활용하여 문자열 별 문자의 갯수를 계산해서 넣어준다.
- result는 결과를 넣을 변수로, ArrayList로 초기화한다.

3. 영문자의 갯수인 0부터 26미만까지 j를 증가시키며 아래를 반복한다.
- min은 최대 갯수인 100보다 큰 101로 초기화하고, 0부터 length 미만까지 i를 증가시키며 min에 min과 count[i][j]의 값 중 작은 값을 넣어준다.
- min이 0보다 클 때 까지 result에 영소문자 j번째 문자를 result에 넣어준다.

4. 반복이 완료되면 공통된 문자들이 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindCommonCharacters.java){:target="_blank"}에서 확인 가능합니다.