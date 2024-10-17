---
title: "Leetcode Java Group Anagrams"
excerpt: "Leetcode - 'Group Anagrams' 문제 Java 풀이"
last_modified_at: 2021-05-30T18:20:00
header:
  image: /assets/images/leetcode/group-anagrams.png
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
[Link](https://leetcode.com/problems/group-anagrams/){:target="_blank"}

# 코드
```java
class Solution {

  private static final char A = 'a';

  public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> result = new HashMap<>();
    for (String str : strs) {
      char[] chars = new char[26];
      for (char chr : str.toCharArray()) {
        chars[chr - A]++;
      }
      String key = String.valueOf(chars);
      if (!result.containsKey(key)) {
        result.put(key, new ArrayList<>());
      }
      result.get(key).add(str);
    }
    return new ArrayList<>(result.values());
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/500813553/){:target="_blank"}

# 설명
1. 주어진 배열 strs에서 동일한 개수의 문자들이 사용된 단어를 그룹으로 생성하여 전체 그룹들을 반환하는 문제이다.

2. 주어진 문제의 결과인 전체 그룹을 담을 Map인 result를 선언한다.

3. 주어진 문자열을 반복하여 그룹을 지어준다.
- 문자의 반복 개수를 파악하기 위해 26 크기인 배열 chars를 정의한다.
- 영문자의 개수는 26개 이므로 크기를 26으로 설정하였다.

4. 반복된 문자 str을 문자 배열로 치환하여 문자의 사용 개수를 확인한다.

5. 사용된 문자의 배열 chars를 key로 사용하기 위해서 String으로 형 변환하여 result에 그룹으로 추가한다.
- Java에서는 객체의 비교에 동일성과 동등성의 검증을 사용한다.
- String을 정의 할 경우 [JVM의 Constant Pool](https://docs.oracle.com/javase/specs/jvms/se7/html/jvms-4.html#jvms-4.4){:target="_blank"}에 저장되고, 활용이 되므로 동일성 검증에도 통과한다.
- 만일 result에 String으로 형 변환한 key가 존재하지 않을 경우, 새로운 ArrayList를 정의하여 key의 값으로 넣어준다.
- 마지막으로, result에 key 값으로 배열을 가져와 반복된 문자 str을 넣어준다.

6. 반복이 완료되면 전체 그룹을 담은 Map의 value들을 새로운 ArrayList에 담아 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/GroupAnagrams.java){:target="_blank"}에서 확인 가능합니다.