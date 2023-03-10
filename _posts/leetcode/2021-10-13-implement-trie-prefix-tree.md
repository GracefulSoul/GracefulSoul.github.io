---
title: "Leetcode Java Implement Trie (Prefix Tree)"
excerpt: "Leetcode Implement Trie (Prefix Tree) Java 풀이"
last_modified_at: 2021-10-13T13:00:00
header:
  image: /assets/images/leetcode/implement-trie-prefix-tree.png
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
[Link](https://leetcode.com/problems/implement-trie-prefix-tree/){:target="_blank"}

# 코드
```java
class Trie {

  private TrieNode root;

  public Trie() {
    root = new TrieNode();
  }

  public void insert(String word) {
    TrieNode node = root;
    for (int idx = 0; idx < word.length(); idx++) {
      int num = word.charAt(idx) - 'a';
      if (node.children[num] == null) {
        node.children[num] = new TrieNode();
      }
      node = node.children[num];
    }
    node.isWord = true;
  }

  public boolean search(String word) {
    return this.match(word, true);
  }

  public boolean startsWith(String prefix) {
    return this.match(prefix, false);
  }

  private boolean match(String str, boolean isWord) {
    TrieNode node = root;
    for (int idx = 0; idx < str.length(); idx++) {
      int num = str.charAt(idx) - 'a';
      if (node.children[num] == null) {
        return false;
      }
      node = node.children[num];
    }
    return isWord ? node.isWord : true;
  }

}

class TrieNode {

  public boolean isWord;
  public TrieNode[] children;

  public TrieNode() {
    this.children = new TrieNode[26];
  }

}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/570408607/){:target="_blank"}

# 설명
1. 탐색 트리의 일종인 [Trie](https://en.wikipedia.org/wiki/Trie){:target="_blank"} 객체를 완성하는 문제이다.
- 생성자인 Trie()는 Trie 객체를 초기화한다.
- 메서드인 insert(String word)는 주어진 문자열 word를 Trie에 삽입한다.
- 메서드인 search(String word)는 주어진 문자열 word가 Trie에 존재하는지 유무를 반환한다.
- 메서드인 startsWith(String prefix)는 기 삽입된 문자열 중 주어진 문자열 prefix로 시작하는 문자열의 유무를 반환한다.

2. 문제 풀이에 필요한 TrieNode 클래스를 정의한다.
- isWord는 해당 단어까지의 문자열이 단어로 존재하는지 여부를 저장하는 변수이다.
- children은 해당 단어까지의 문자열 이후의 문자열을 이어주기 위한 변수로, 객체 생성 시 다음 문자를 저장하기 위해 알파벳의 개수인 26 크기의 TrieNode 배열로 초기화 한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- root는 Trie의 가장 최상위 노드를 저장하기 위한 변수이다.

4. 주어진 생성자인 Trie()를 완성한다.
- 전역 변수인 TreeNode를 초기화 시켜 순차적인 문자열 입력이 가능하도록 한다.

5. 주어진 메서드인 insert(String word)를 완성한다.
- 전역 변수인 root를 지역 변수인 node에 복사해준다.
  - 주어진 root를 점층적으로 내려가며 단어의 완성을 할 때, 기존 값들을 보호하기 위해서 node에 복사하여 node를 변경하며 수행하는 것이다.
- 주어진 word를 한 문자씩 반복하여 node 아래로 문자열을 TrieNode에 연결시켜준다.
  - 주어진 word의 idx번째 문자에서 'a'를 빼 0(a) ~ 25(z))까지 숫자를 num에 넣어준다.
  - node.children의 num번째 TrieNode가 null인 경우, 하위 문자열을 이어주기 위해서 새 TrieNode를 넣어준다.
  - node에 node.children[num]을 넣어 이후 문자들을 이용하여 Trie를 완성한다.
- 반복이 완료되면 마지막 TrieNode의 isWord를 true로 바꾸어 해당 문자열까지 입력된 단어임을 체크해준다.

6. 주어진 메서드인 search(String word)와 startsWith(String prefix)는 동일하게 검색을 수행하는 메서드로, 공통된 역할을 수행하는 match(String str, boolean isWord)를 먼저 만들어준다.
- 전역 변수인 root를 지역 변수인 node에 복사해준다.
  - 주어진 root를 점층적으로 내려가며 단어를 검색 할 때, 기존 값들을 보호하기 위해서 node에 복사하여 node를 변경하며 수행하는 것이다.
- 주어진 str을 한 문자씩 반복하여 해당 문자열이 존재하는지 탐색한다.
  - 주어진 str의 idx번째 문자에서 'a'를 빼 0(a) ~ 25(z)까지 숫자를 num에 넣어준다.
  - node.children의 num번째 TrieNode가 null인 경우, 해당 문자열이 존재하지 않으므로 false를 반환한다.
  - node에 node.children[num]을 넣어 이후 문자들을 계속 탐색한다.
- 반복이 완료되면 isWord에 따라 각 값을 반환한다.
  - isWord가 true인 경우, node.isWord의 값을 통해 입력된 값인지 여부를 반환한다.
  - isWord가 false인 경우, 입력된 값인지 여부에 상관없이 true를 반환한다.

7. 주어진 메서드인 search(String word)를 완성한다.
- 6번에서 완성한 match(String str, boolean isWord)를 이용하여, isWord를 true로 줌으로써 입력된 값이 존재하는지 여부를 반환한다.

8. 주어진 메서드인 startsWith(String prefix)를 완성한다.
- 6번에서 완성한 match(String str, boolean isWord)를 이용하여, isWord를 false로 줌으로써 입력된 값인지 유무에 상관없이 존재하는지 여부를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ImplementTrie.java){:target="_blank"}에서 확인 가능합니다.