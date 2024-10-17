---
title: "Leetcode Java Lexicographically Smallest Equivalent String"
excerpt: "Leetcode Medium - 'Lexicographically Smallest Equivalent String' 문제 Java 풀이"
last_modified_at: 2024-03-26T18:30:00
header:
  image: /assets/images/leetcode/lexicographically-smallest-equivalent-string.png
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
[Link](https://leetcode.com/problems/lexicographically-smallest-equivalent-string/){:target="_blank"}

# 코드
```java
class Solution {

  public String smallestEquivalentString(String s1, String s2, String baseStr) {
    int[] graph = new int[26];
    for (int i = 0; i < 26; i++) {
      graph[i] = i;
    }
    char[] s1CharArray = s1.toCharArray();
    char[] s2CharArray = s2.toCharArray();
    for (int i = 0; i < s1.length(); i++) {
      int j = this.find(graph, s1CharArray[i] - 'a');
      int k = this.find(graph, s2CharArray[i] - 'a');
      if (k < j) {
        graph[j] = k;
      } else {
        graph[k] = j;
      }
    }
    StringBuilder sb = new StringBuilder();
    for (char c : baseStr.toCharArray()) {
      sb.append((char) ('a' + this.find(graph, c - 'a')));
    }
    return sb.toString();
  }

  private int find(int[] graph, int index) {
    while (graph[index] != index) {
      index = graph[index];
    }
    return index;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/lexicographically-smallest-equivalent-string/submissions/1214287091/){:target="_blank"}

# 설명
1. 등치 문자열인 s1과 s2의 등가 정보를 이용하여, 사전적으로 가장 작은 등가 문자열인 baseStr을 반환하는 문제이다.
- 등치 문자열은 $s1 = abc$, $s2 = cde$일 때,  "a" == "c", "b" == "d", "c" == "e"를 만족한다.
- 위를 이용하여 baseStr이 "eed" 문자열일 때, "acd"와 "aab"는 등가 문자열이며 이 중 "aab"는 사전적으로 가장 작은 등가 문자열이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- graph는 등치 문자열의 영문자 위치 값을 저장할 변수로, 26 크기의 정수 배열로 초기화하여 각 위치에 0부터 25까지 넣어준다.
- s1CharArray와 s2CharArray는 s1과 s2를 문자 배열로 저장한 변수이다.

3. graph의 index번째 문자의 등치 문자열 탐색에 필요한 find(int[] graph, int index) 메서드를 정의한다.
- graph의 index번째 값이 index가 아닐 때 까지 index에 graph[index] 값을 넣어준 후, index를 반환한다.

4. 0부터 s1의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- j와 k에 s1CharArray와 s2CharArray의 i번째 문자의 영문자 순서를 이용하여 find 메서드를 수행한 결과를 각각 넣어준다.
- k가 j보다 작은 경우 사전적인 순서대로 저장해야 하므로, graph[j]에 k를 아니면 grpah[k]에 j를 넣어준다.

5. 반복이 완료되면 최종 문자열을 만들기 위한 sb를 StringBuilder로 초기화한 후 baseStr의 각 문자를 순차적으로 c에 넣어 아래를 수행한다.
- sb에 'a'에 c의 영문자 순서를 이용하여 find 메서드를 수행한 결과를 더하여 이어준다.

6. 반복이 완료되면 저장된 sb를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LexicographicallySmallestEquivalentString.java){:target="_blank"}에서 확인 가능합니다.