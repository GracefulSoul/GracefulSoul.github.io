---
title: "Leetcode Java Design Add and Search Words Data Structure"
excerpt: "Leetcode Design Add and Search Words Data Structure Java 풀이"
last_modified_at: 2021-10-16T13:00:00
header:
  image: /assets/images/leetcode/design-add-and-search-words-data-structure.png
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
[Link](https://leetcode.com/problems/design-add-and-search-words-data-structure/){:target="_blank"}

# 코드
```java
class WordDictionary {

  private TrieNode root;

  public WordDictionary() {
    this.root = new TrieNode();
  }

  public void addWord(String word) {
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
    return this.match(root, word.toCharArray(), 0);
  }

  private boolean match(TrieNode node, char[] charArray, int index) {
    if (index == charArray.length) {
      return node.isWord;
    }
    if (charArray[index] == '.') {
      for (int idx = 0; idx < node.children.length; idx++) {
        if (node.children[idx] != null && this.match(node.children[idx], charArray, index + 1)) {
          return true;
        }
      }
    } else {
      int num = charArray[index] - 'a';
      return node.children[num] != null && this.match(node.children[num], charArray, index + 1);
    }
    return false;
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
 * Your WordDictionary object will be instantiated and called as such:
 * WordDictionary obj = new WordDictionary();
 * obj.addWord(word);
 * boolean param_2 = obj.search(word);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/571923823/){:target="_blank"}

# 설명
1. 지난번 [Implement Trie (Prefix Tree)](../implement-trie-prefix-tree)와 유사한 문제로, WordDictionary 클래스를 완성하는 문제이다.
- 단, 주어진 문자열 word에 "."이 들어간 경우, 어느 문자열이 들어와도 상관이 없다.
- 생성자인 WordDictionary()는 WordDictionary 객체를 초기화 한다.
- 메서드인 addWord(word)는 주어진 문자열 word를 WordDictionary 객체에 저장한다.
- 메서드인 search(word)는 주어진 문자열 word가 WordDictionary 객체에 주입된 문자열 중 존재하는지 유무를 반환한다.

2. 문제 풀이에 필요한 TrieNode 클래스를 정의한다.
- isWord는 해당 단어까지의 문자열이 단어로 존재하는지 여부를 저장하는 변수이다.
- children은 해당 단어까지의 문자열 이후의 문자열을 이어주기 위한 변수로, 객체 생성 시 다음 문자를 저장하기 위해 알파벳의 갯수인 26 크기의 TrieNode 배열로 초기화 한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- root는 주어진 문제를 Trie를 이용하여 풀기위해, Trie의 가장 최상위 노드를 저장하기 위한 변수이다.

4. 주어진 생성자인 WordDictionary()를 완성한다.
- 전역 변수인 TreeNode인 root를 초기화 시켜 순차적인 문자열 입력이 가능하도록 한다.

5. 주어진 메서드인 addWord(word)를 완성한다.
- 전역 변수인 root를 지역 변수인 node에 복사해준다.
  - 주어진 root를 점층적으로 내려가며 단어의 완성을 할 때, 기존 값들을 보호하기 위해서 node에 복사하여 node를 변경하며 수행하는 것이다.
- 주어진 word를 한 문자씩 반복하여 node 아래로 문자열을 TrieNode에 연결시켜준다.
  - 주어진 word의 idx번째 문자에서 'a'를 빼 0(a) ~ 25(z))까지 숫자를 num에 넣어준다.
  - node.children의 num번째 TrieNode가 null인 경우, 하위 문자열을 이어주기 위해서 새 TrieNode를 넣어준다.
  - node에 node.children[num]을 넣어 이후 문자들을 이용하여 Trie를 완성한다.
- 반복이 완료되면 마지막 TrieNode의 isWord를 true로 바꾸어 해당 문자열까지 입력된 단어임을 체크해준다.

6. 주어진 메서드인 search(word)를 완성하려면 "."인 경우 node.children을 전체 순회해야 하기 때문에, 재귀 호출을 위한 match(node, charArray, index)를 먼저 완성한다.
- index가 charArray.length와 동일한 경우 검색 문자열의 마지막이기 때문에, 주입된 문자열인지 여부를 저장하는 node.isWord를 반환한다.
- charArray[index]의 값이 "."인 경우, 아래를 수행한다.
  - node.children을 모두 확인하여 node.children[idx]이 존재하는 경우를 우선 확인한다.
  - 이후 재귀 호출을 이용하여 이후 문자열들이 존재하고 주입된 문자열인 경우, true를 반환한다.
- charArray[index]의 값이 "."이 아닌 경우, 아래를 수행한다.
  - 지역 변수 num을 정의하여 반복 사용되는 $charArray[index] - 'a'$를 넣어준다.
  - node.children을 모두 확인하여 node.children[num]이 존재하는 경우를 우선 확인한다.
  - 이후 재귀 호출을 이용하여 이후 문자열들이 존재하고 주입된 문자열인지 확인하여 해당 결과를 반환한다.
- 그 외의 경우 주입된 문자열 중에 word가 존재하지 않는다는 의미이므로, false를 반환한다.

7. 주어진 메서드인 search(word)를 완성한다.
- 6에서 완성한 match(node, charArray, index) 메서드를 이용하여 첫 문자열부터 확인하기 위해 index를 0부터 검색한 결과를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DesignAddAndSearchWordsDataStructure.java){:target="_blank"}에서 확인 가능합니다.