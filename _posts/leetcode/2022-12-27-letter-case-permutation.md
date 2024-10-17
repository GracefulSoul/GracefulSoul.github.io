---
title: "Leetcode Java Letter Case Permutation"
excerpt: "Leetcode - 'Letter Case Permutation' 문제 Java 풀이"
last_modified_at: 2022-12-27T15:45:00
header:
  image: /assets/images/leetcode/letter-case-permutation.png
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
[Link](https://leetcode.com/problems/letter-case-permutation){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> letterCasePermutation(String s) {
    List<String> result = new ArrayList<>();
    this.dfs(result, s.toCharArray(), 0);
    return result;
  }

  private void dfs(List<String> result, char[] charArray, int index) {
    if (index == charArray.length) {
      result.add(new String(charArray));
    } else if (Character.isDigit(charArray[index])) {
      this.dfs(result, charArray, index + 1);
    } else {
      charArray[index] = Character.toLowerCase(charArray[index]);
      this.dfs(result, charArray, index + 1);
      charArray[index] = Character.toUpperCase(charArray[index]);
      this.dfs(result, charArray, index + 1);
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/letter-case-permutation/submissions/866187282/){:target="_blank"}

# 설명
1. s를 이용하여 영문 대소문자를 변환하여 만들 수 있는 모든 문자열을 만드는 문제이다.

2. 결과를 넣을 result를 ArrayList로 초기화 시키고, 3번에서 정의한 dfs(List<String> result, char[] charArray, int index)에 s를 문자 배열로 변환하고 index를 0으로 수행한다.

3. DFS 방식으로 문자열을 만들 dfs(List<String> result, char[] charArray, int index) 메서드를 정의한다.
- index가 charArray의 길이와 동일하면 문자열이 완성되었으므로, result에 charArray를 문자열로 변환하여 넣어준다.
- charArray의 index번째 문자가 숫자인 경우, index를 증가시켜 재귀 호출을 수행한다.
- 위의 경우가 아니라면 아래를 수행한다.
  - charArray의 index번째 문자를 소문자로 변환하고 index를 증가시켜 재귀 호출을 수행한다.
  - charArray의 index번째 문자를 대문자로 변환하고 index를 증가시켜 재귀 호출을 수행한다.

4. 수행이 완료되어 가능한 문자열이 들어간 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LetterCasePermutation.java){:target="_blank"}에서 확인 가능합니다.