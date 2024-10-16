---
title: "Leetcode Java Sum of Prefix Scores of Strings"
excerpt: "Leetcode Sum of Prefix Scores of Strings Java"
last_modified_at: 2024-09-25T18:30:00
header:
  image: /assets/images/leetcode/sum-of-prefix-scores-of-strings.png
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
[Link](https://leetcode.com/problems/sum-of-prefix-scores-of-strings/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] sumPrefixScores(String[] words) {
    TrieNode trieNode = new TrieNode();
    for (String word : words) {
      TrieNode temp = trieNode;
      for (char c : word.toCharArray()) {
        int num = c - 'a';
        if (temp.children[num] == null) {
          temp.children[num] = new TrieNode();
        }
        temp.children[num].sum++;
        temp = temp.children[num];
      }
    }
    int i = 0;
    int[] result = new int[words.length];
    for (String word : words) {
      TrieNode temp = trieNode;
      int sum = 0;
      for (char c : word.toCharArray()) {
        int num = c - 'a';
        sum += temp.children[num].sum;
        temp = temp.children[num];
      }
      result[i++] = sum;
    }
    return result;
  }

}
class TrieNode {

	public int sum;
	public TrieNode[] children;

	public TrieNode() {
		this.sum = 0;
		this.children = new TrieNode[26];
	}

}
```

# 결과
[Link](https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/submissions/1400542081/){:target="_blank"}

# 설명
1. words 내 각 단어 별 접두사가 동일한 words의 문자 갯수를 동일한 위치의 배열로 반환하는 문제이다.

2. TrieNode는 각 단어에 해당하는 문자 갯수를 저장할 객체이다.
- sum은 현재 위치에 해당하는 문자의 합계를 계산할 변수이다.
- children은 현재 위치 이후로 존재하는 문자를 이어주기 위한 변수이다.
- 생성자인 TrieNode()는 객체를 초기화할 메서드로, sum에 0, children에 영문자 갯수인 26 크기의 TrieNode 배열로 초기화한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- trieNode는 words의 문자들 내 접두사를 순차적으로 [Trie](https://en.wikipedia.org/wiki/Trie){:target="_blank"}를 활용하여 넣을 변수로, words의 각 단어들로 해당 객체를 초기화한다.
- i는 결과 문자열의 위치 변수로, 0으로 초기화한다.
- result는 결과를 저장할 배여롤, words 길이의 정수 배열로 초기화한다.

4. words를 순차적으로 word에 넣어 trieNode에서 접두사 별 합계를 더해 result의 각 위치에 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SumOfPrefixScoresOfStrings.java){:target="_blank"}에서 확인 가능합니다.