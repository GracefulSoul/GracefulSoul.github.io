---
title: "Leetcode Java Smallest Subsequence of Distinct Characters"
excerpt: "Leetcode Smallest Subsequence of Distinct Characters Java"
last_modified_at: 2024-04-15T19:00:00
header:
  image: /assets/images/leetcode/smallest-subsequence-of-distinct-characters.png
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
[Link](https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/){:target="_blank"}

# 코드
```java
class Solution {

  public String smallestSubsequence(String s) {
    int[] count = new int[26];
    for (char c : s.toCharArray()) {
      count[c - 'a']++;
    }
    boolean[] visited = new boolean[26];
    Stack<Character> stack = new Stack<>();
    for (char c : s.toCharArray()) {
      count[c - 'a']--;
      if (visited[c - 'a']) {
        continue;
      }
      while (!stack.isEmpty() && c < stack.peek() && 0 < count[stack.peek() - 'a']) {
        visited[stack.pop() - 'a'] = false;
      }
      stack.push(c);
      visited[c - 'a'] = true;
    }
    StringBuilder sb = new StringBuilder();
    for (char c : stack) {
      sb.append(c);
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/smallest-subsequence-of-distinct-characters/submissions/1232939894/){:target="_blank"}

# 설명
1. 문자열 s의 문자들을 한 번만 포함된 사전적으로 가장 작은 부분 수열을 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 문자열 s의 문자 갯수를 저장할 배열로, 영문자 갯수인 26 크기의 정수 배열로 초기화하여 s의 문자열 내 각 문자의 위치에 갯수를 더해준다.
- visited는 사용한 문자인지 검증하기 위한 배열로, 영문자 갯수인 26 크기의 부울 배열로 초기화한다.
- stack은 결과 문자열을 만들기 위한 변수로, Stack으로 초기화한다.

3. s의 문자들을 순차적으로 c에 넣고 아래를 수행한다.
- count의 해당 문자 순서에 해당하는 갯수를 차감시킨다.
- visited의 해당 문자 순서에 해당하는 값이 true이면 이미 사용했으므로, 다음 반복을 수행한다.
- 아래의 경우를 모두 만족하면, visited 내 stack의 가장 앞 문자에 해당하는 순서의 값을 false로 바꿔준다.
  - stack 내 문자들이 존재하는 경우.
  - stack의 가장 앞 문자가 c보다 사전적으로 큰 경우.
  - count의 stack의 가장 앞 문자에 해당하는 순서의 값이 0보다 큰 경우.
- stack에 c를 넣은 후 visited의 c에 해당하는 순서의 값을 true로 바꾸어준다.

4. 위의 반복이 완료되면 stack에 저장된 값을 순차적으로 꺼내 문자열로 만들어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SmallestSubsequenceOfDistinctCharacters.java){:target="_blank"}에서 확인 가능합니다.