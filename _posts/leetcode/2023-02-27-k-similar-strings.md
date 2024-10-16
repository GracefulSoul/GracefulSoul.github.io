---
title: "Leetcode Java K-Similar Strings"
excerpt: "Leetcode K-Similar Strings Java"
last_modified_at: 2023-02-27T19:30:00
header:
  image: /assets/images/leetcode/k-similar-strings.png
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
[Link](https://leetcode.com/problems/k-similar-strings){:target="_blank"}

# 코드
```java
class Solution {

  private int result;
  private int length;

  public int kSimilarity(String s1, String s2) {
    this.result = Integer.MAX_VALUE;
    this.length = s1.length();
    this.dfs(s1.toCharArray(), s2.toCharArray(), 0, 0);
    return this.result;
  }

  private void dfs(char[] s1CharArray, char[] s2CharArray, int start, int curr) {
    if (curr >= this.result) {
      return;
    }
    for (int i = start; i < this.length; i++) {
      if (s1CharArray[i] != s2CharArray[i]) {
        for (int j = i + 1; j < this.length; j++) {
          if (s1CharArray[i] == s2CharArray[j] && s1CharArray[j] != s2CharArray[j]) {
            this.swap(s2CharArray, i, j);
            this.dfs(s1CharArray, s2CharArray, i + 1, curr + 1);
            this.swap(s2CharArray, i, j);
            if (s1CharArray[j] == s2CharArray[i]) {
              break;
            }
          }
        }
        return;
      }
    }
    this.result = Math.min(curr, this.result);
  }

  private void swap(char[] charArray, int i, int j) {
    char c = charArray[i];
    charArray[i] = charArray[j];
    charArray[j] = c;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/k-similar-strings/submissions/905851931/){:target="_blank"}

# 설명
1. s1을 s2로 변환하기 위한 최소 스왑 횟수를 구하는 문제이다.
- 단, 모든 문자는 ['a', 'b', 'c', 'd', 'e', 'f']로 이루어져있다.
- s1은 s2의 [Anagram](https://en.wikipedia.org/wiki/Anagram){:target="_blank"}이다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- result는 스왑 횟수를 계산하기 위한 변수이다.
- length는 문자열의 길이을 저장하기 위하 변수이다.

3. result에 정수의 최댓값을, length에 s1의 길이를 저장하고 4번에서 정의한 dfs(char[] s1CharArray, char[] s2CharArray, int start, int curr) 메서드를 s1과 s2를 문자 배열로 변환하고 start와 curr에 0을 넣어 수행한다.

4. DFS 방식으로 문자를 스왑하며 탐색할 dfs(char[] s1CharArray, char[] s2CharArray, int start, int curr) 메서드를 정의한다.
- curr이 result보다 크거나 같은 경우, 현재 위치에서 수행 가능한 스왑 횟수를 넘어섰으므로 수행을 그만한다.
- start부터 length 미만까지 i를 증가시키며 아래를 수행한다.
  - s1CharArray와 s2CharArray의 i번째 문자가 같으면 반복을 계속한다.
  - 그렇지 않으면 $i + 1$부터 length미만까지 j를 증가시키며 s1CharArray의 i번째 문자와 s2CharArray의 j번째 문자가 같고 두 배열의 j번째 문자가 동일하지 않는 경으면 해당 문자를 바꿔서 start에 $i + 1$, curr에 $curr + 1$을 이용하여 재귀 호출을 수행하고 바꾼 문자를 원 위치로 돌린 후, s1CharArray의 j번째 문자와 s2CharArray의 i번째 문자가 같으면 반복을 중지하고 i에 대한 반복 위치에서 다음 반복을 수행한다.
- 반복이 완료되면 result에 curr과 result 중 작은 값을 넣어준다.

5. 반복이 완료되면 최소 스왑 횟수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KSimilarStrings.java){:target="_blank"}에서 확인 가능합니다.