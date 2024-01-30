---
title: "Leetcode Java Stream of Characters"
excerpt: "Leetcode Stream of Characters Java"
last_modified_at: 2024-01-30T20:10:00
header:
  image: /assets/images/leetcode/stream-of-characters.png
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
[Link](https://leetcode.com/problems/stream-of-characters){:target="_blank"}

# 코드
```java
class StreamChecker {

  private TrieNode root;
  private StringBuilder sb;

  public StreamChecker(String[] words) {
    this.root = new TrieNode();
    this.sb = new StringBuilder();
    for (String word : words) {
      TrieNode node = this.root;
      char[] charArray = word.toCharArray();
      int length = charArray.length;
      for (int i = length - 1; i >= 0; i--) {
        int index = charArray[i] - 'a';
        if (node.children[index] == null) {
          node.children[index] = new TrieNode();
        }
        node = node.children[index];
      }
      node.isWord = true;
    }
  }

  public boolean query(char letter) {
    this.sb.append(letter);
    TrieNode node = this.root;
    for (int i = this.sb.length() - 1; i >= 0 && node != null; i--) {
      node = node.children[this.sb.charAt(i) - 'a'];
      if (node != null && node.isWord) {
        return true;
      }
    }
    return false;
  }

}

public class TrieNode {

  public boolean isWord;
  public TrieNode[] children;

  public TrieNode() {
    this.children = new TrieNode[26];
  }

}

/**
 * Your StreamChecker object will be instantiated and called as such:
 * StreamChecker obj = new StreamChecker(words);
 * boolean param_1 = obj.query(letter);
 */
```

# 결과
[Link](https://leetcode.com/problems/stream-of-characters/submissions/1160972457/){:target="_blank"}

# 설명
1. words로 초기화된 문자 스트림에서 순차적으로 문자를 이어줄 때, 접미사가 words 내 존재하는지 검증하는 문제이다.
- 생성자인 StreamChecker(String[] words)는 words를 이용하여 객체를 초기화하는 역할을 수행한다.
- 메서드인 query(char letter)는 letter를 문자열로 계속 이어주고, 접미사가 words 내 존재하는지 여부를 반환한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- root는 문자를 [Trie](https://en.wikipedia.org/wiki/Trie){:target="_blank"}를 활용하여 저장할 변수이다.
- sb는 query 메서드를 통해 입력된 문자를 순차적으로 이어줄 변수이다.

3. 생성자인 StreamChecker(String[] words)를 정의한다.
- root에 아래의 값을 가진 TrieNode를 초기화하여 넣어준다.
  - isWord는 현재 위치까지 문자로 존재하는지 여부를 나타내기 위한 값을 저장하는 변수이다.
  - children은 현재 문자 이후에 나타날 문자를 새 TrieNode로 이어줄 변수로, 영문자의 갯수인 26 크기로 초기화 하여 넣어준다.
- sb는 동적 문자열의 생성을 위해 StringBuilder로 초기화한다.
- words를 반복하여 root의 children에 각 문자열의 역순으로 TrieNode를 이어서 넣어주면서, 시작되는 문자 위치에 isWord를 true로 해당 문자열이 존재하는 것을 체크해준다.

4. 메서드인 query(char letter)를 정의한다.
- sb에 letter를 이어준 후, node에 root를 넣어준다.
- sb의 마지막 위치부터 처음이면서, node가 null이 아닐 때 까지 i를 감소시키며 아래를 반복한다.
  - node에 node의 children 중 sb의 i번째 문자 순서의 TrieNode를 넣어준다.
  - node가 null이 아니면서 isWord인 초기에 주입된 words에 포함된 단어인 경우, true를 반환한다.
- 반복이 완료되면 sb의 접미사가 words 내 존재하지 않으므로, false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StreamOfCharacters.java){:target="_blank"}에서 확인 가능합니다.