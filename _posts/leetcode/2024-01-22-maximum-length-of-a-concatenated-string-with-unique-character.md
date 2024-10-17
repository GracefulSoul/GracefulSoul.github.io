---
title: "Leetcode Java Maximum Length of a Concatenated String with Unique Characters"
excerpt: "Leetcode Medium - 'Maximum Length of a Concatenated String with Unique Characters' 문제 Java 풀이"
last_modified_at: 2024-01-23T20:00:00
header:
  image: /assets/images/leetcode/maximum-length-of-a-concatenated-string-with-unique-character.png
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
[Link](https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters){:target="_blank"}

# 코드
```java
class Solution {

  private int result;

  public int maxLength(List<String> arr) {
    this.result = 0;
    this.dfs(arr, "", 0);
    return this.result;
  }

  private void dfs(List<String> arr, String s, int index) {
    boolean isUnique = this.validate(s);
    if (isUnique) {
      this.result = Math.max(this.result, s.length());
    }
    if (index == arr.size() || !isUnique) {
      return;
    }
    for (int i = index; i < arr.size(); i++) {
      this.dfs(arr, s + arr.get(i), i + 1);
    }
  }

  private boolean validate(String s) {
    Set<Character> set = new HashSet<>();
    for (char c : s.toCharArray()) {
      if (set.contains(c)) {
        return false;
      }
      set.add(c);
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/submissions/1154513348/){:target="_blank"}

# 설명
1. arr의 각 요소들을 순차적으로 이어서 고유 문자들로만 이루어진 문자열을 만들 때, 가능한 최대 길이를 구하는 문제이다.

2. result는 가능한 최대 길이를 저장할 전역 변수이다.

3. result를 0으로 초기화하고 4번에서 정의한 dfs(List<String> arr, String s, int index) 메서드에 ""과 0을 같이 넣어 수행한다.

4. DFS 방식으로 탐색할 dfs(List<String> arr, String s, int index) 메서드를 정의한다.
- isUnique는 s의 문자열이 고유한 문자들로 이루어졌는지 검증한 변수로, validate(String s) 메서드를 수행하여 검증한 결과를 넣어준다.
- isUnique가 true인 고유 문자들로 구성되어 있다면, result에 result와 s의 길이 중 큰 값인 길이를 넣어준다.
- index가 arr의 길이와 동일하거나 isUnique가 false인 고유 문자열이 아닌 경우, 수행을 중단한다.
- index부터 arr의 길이까지 i를 증가시키며 s에 s와 arr의 i번째 문자를 이어주고, index에 $i + 1$을 넣어 재귀 호출을 순차적으로 수행한다.

5. 4번의 수행이 완료되면 최대 길이가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumLengthOfAConcatenatedStringwithUniqueCharacters.java){:target="_blank"}에서 확인 가능합니다.