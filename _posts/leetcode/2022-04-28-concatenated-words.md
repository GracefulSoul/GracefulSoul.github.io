---
title: "Leetcode Java Concatenated Words"
excerpt: "Leetcode Concatenated Words Java 풀이"
last_modified_at: 2022-04-28T13:00:00
header:
  image: /assets/images/leetcode/concatenated-words.png
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
[Link](https://leetcode.com/problems/concatenated-words/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> findAllConcatenatedWordsInADict(String[] words) {
    Arrays.sort(words, (a, b) -> a.length() - b.length());
    TrieNode root = new TrieNode();
    List<String> result = new ArrayList<>();
    for (String word : words) {
      if (this.isAddable(root, word)) {
        result.add(word);
      }
    }
    return result;
  }

  private boolean isAddable(TrieNode root, String word) {
    TrieNode curr = root;
    for (int idx = 0; idx < word.length(); idx++) {
      int num = word.charAt(idx) - 'a';
      if (curr.children[num] == null) {
        curr.children[num] = new TrieNode();
      }
      curr = curr.children[num];
      if (curr.isWord && idx < word.length() - 1 && this.isContains(root, word.substring(idx + 1))) {
        return true;
      }
    }
    curr.isWord = true;
    return false;
  }

  private boolean isContains(TrieNode root, String word) {
    TrieNode curr = root;
    for (int idx = 0; idx < word.length(); idx++) {
      int num = word.charAt(idx) - 'a';
      if (curr.children[num] == null) {
        return false;
      }
      curr = curr.children[num];
      if (curr.isWord && idx < word.length() - 1 && this.isContains(root, word.substring(idx + 1))) {
        return true;
      }
    }
    return curr.isWord;
  }

}

class TrieNode {

  public boolean isWord;
  public TrieNode[] children;

  public TrieNode() {
    this.children = new TrieNode[26];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/688904538/){:target="_blank"}

# 설명
1. words 내 문자들을 2개 이상 조합해서 나올 수 있는 모든 문자열을 구하는 문제이다.

2. 문제 풀이에 필요한 TrieNode 클래스를 정의한다.
- isWord는 해당 단어까지의 문자열이 단어로 존재하는지 여부를 저장하는 변수이다.
- children은 해당 단어까지의 문자열 이후의 문자열을 이어주기 위한 변수로, 객체 생성 시 다음 문자를 저장하기 위해 알파벳의 개수인 26 크기의 TrieNode 배열로 초기화 한다.

3. words 내 단어들을 길이 별로 정렬을 수행한다.

4. 문제 풀이에 필요한 변수를 정의한다.
- root는 문자를 [Trie](https://en.wikipedia.org/wiki/Trie){:target="_blank"}로 구성하기 위해 TrieNode를 새로 생성해서 넣어준다.
- reulst는 조합한 문자열을 넣어주기 위한 변수로, ArrayList로 정의한다.

5. words내 단어들을 모두 반복한다.
- 6번에서 정의한 isAddable(TrieNode root, String word)가 true인 경우, reulst에 word를 넣어준다.

6. 결과에 포함할 수 있는지를 검증하기 위한 isAddable(TrieNode root, String word) 메서드를 정의한다.
- root를 curr에 넣어준다.
- 0부터 word의 길이 전까지 idx를 증가시키며 아래를 수행한다.
  - num에 word의 idx번째 문자를 'a'를 뺀 영소문자 인덱스를 넣어준다.
  - curr 내 children의 num번째 값이 null인 경우, 새 TrieNode를 넣어 초기화한다.
  - curr에 children의 num번째 TrieNode를 넣어 단어를 넣을 준비를 한다.
  - curr의 isWord가 true이고 마지막 단어가 아니며 7번에서 정의한 isContains(TrieNode root, String word)에 word를 $idx + 1$번째 글자부터 끝까지의 단어로 수행한 결과가 true이면 결과에 추가할 단어가 되므로, true를 반환한다.
- 반복이 완료되면 curr의 isWord를 true로 바꾸고, false를 반환한다.

7. 6번과 유사하지만 해당 단어가 포함되어있는지 검증하기 위한 isContains(TrieNode root, String word) 메서드를 정의한다.
- root를 curr에 넣어준다.
- 0부터 word의 길이 전까지 idx를 증가시키며 아래를 수행한다.
  - num에 word의 idx번째 문자를 'a'를 뺀 영소문자 인덱스를 넣어준다.
  - curr 내 children의 num번째 값이 null인 경우 존재하지 않으므로, false를 반환한다.
  - curr에 children의 num번째 TrieNode를 넣어 검증을 수행할 준비를 한다.
  - curr의 isWord가 true이고 마지막 단어가 아니며 7번에서 정의한 isContains(TrieNode root, String word)에 word를 $idx + 1$번째 글자부터 끝까지의 단어로 수행한 결과가 true이면 포함된 단어이므로, true를 반환한다.
- 반복이 완료되면 curr의 isWord를 반환한다.

8. 반복이 완료되면 부분 문자열을 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConcatenatedWords.java){:target="_blank"}에서 확인 가능합니다.