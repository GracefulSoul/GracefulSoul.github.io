---
title: "Leetcode Java Prefix and Suffix Search"
excerpt: "Leetcode Prefix and Suffix Search Java"
last_modified_at: 2022-12-01T12:50:00
header:
  image: /assets/images/leetcode/prefix-and-suffix-search.png
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
[Link](https://leetcode.com/problems/prefix-and-suffix-search){:target="_blank"}

# 코드
```java
class TrieNode {

  public int index;
  public TrieNode[] children;

  public TrieNode() {
    this.children = new TrieNode[27];
  }

}

class WordFilter {

  private TrieNode root = new TrieNode();

  public WordFilter(String[] words) {
    for (int i = 0; i < words.length; i++) {
      char[] charArray = (words[i] + "{" + words[i]).toCharArray();
      for (int j = 0; j < charArray.length; j++) {
        TrieNode temp = this.root;
        for (int k = j; k < charArray.length; k++) {
          int num = charArray[k] - 'a';
          if (temp.children[num] == null) {
            temp.children[num] = new TrieNode();
          }
          temp = temp.children[num];
          temp.index = i;
        }
      }
    }
  }

  public int f(String pref, String suff) {
    char[] charArray = (suff + "{" + pref).toCharArray();
    TrieNode temp = this.root;
    for (char c : charArray) {
      temp = temp.children[c - 'a'];
      if (temp == null) {
        return -1;
      }
    }
    return temp.index;
  }

}

/**
 * Your WordFilter object will be instantiated and called as such:
 * WordFilter obj = new WordFilter(words);
 * int param_1 = obj.f(pref,suff);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/853124162/){:target="_blank"}

# 설명
1. 접두사와 접미사를 이용하여 단어 검색을 수행하는 사전을 만드는 문제이다.
- 생성자인 WordFilter(string[] words)는 words를 이용하여 사전을 초기화하는 역할을 수행한다.
- 메서드인 f(string pref, string suff)는 접두사인 pref와 접미사인 suff를 이용하여 일치하는 단어들의 위치 중 가장 큰 위치 값을 반환한다.

2. 단어를 저장 및 검색하기 위한 TrieNode를 정의한다.
- index는 words 내 위치 값을 저장하기 위한 변수이다.
- children은 다음 문자를 이어주기 위한 변수이다.
- 생성자인 TrieNode()를 호출하면 children에 영소문자 26 문자와 구분 기호 1 문자을 이용하기 위해 27 크기의 TrieNode 배열로 초기화한다.

3. root는 생성자를 통해 입력된 전체 문자열을 순차적으로 저장할 TrieNode 객체이다.

4. 생성자인 WordFilter(string[] words)를 완성한다.
- 0 부터 words의 길이 미만까지 i를 증가시키며 아래를 수행한다.
  - charArray에 words의 i번째 문자를 구분 문자인 "{" 단어 앞뒤로 이어준 문자열의 문자 배열을 저장한다.
  - 구분 문자를 "{"로 사용하는 이유는 영소문자 "z" 이후에 나오는 단어이므로, 순차적으로 children에 저장하기 수월하기 때문이다.
  - 앞에서 만들어준 charArray를 이용하여 temp에 차례대로 TrieNode로 연결시켜준다.

5. 메서드인 f(string pref, string suff)를 완성한다.
- charArray에 구분 문자인 "{" 단어 앞뒤로 suff와 pref를 이어준 문자열의 문자 배열을 저장한다.
- temp에 root를 넣어주고, charArray를 이용하여 TrieNode를 순차 탐색한다.
- 탐색 중 문자를 찾지 못하면 -1을, 탐색 완료되면 temp의 index를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PrefixAndSuffixSearch.java){:target="_blank"}에서 확인 가능합니다.