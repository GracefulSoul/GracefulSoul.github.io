---
title: "Leetcode Java Word Search II"
excerpt: "Leetcode - 'Word Search II' 문제 Java 풀이"
last_modified_at: 2021-10-17T12:00:00
header:
  image: /assets/images/leetcode/word-search-ii.png
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
[Link](https://leetcode.com/problems/word-search-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public List<String> findWords(char[][] board, String[] words) {
    List<String> result = new ArrayList<>();
    TrieNode root = this.initTrieNode(words);
    for (int i = 0; i < board.length; i++) {
      for (int j = 0; j < board[i].length; j++) {
        this.dfs(board, i, j, root, result);
      }
    }
    return result;
  }

  private void dfs(char[][] board, int i, int j, TrieNode node, List<String> result) {
    char c = board[i][j];
    int num = c - 'a';
    if (c == '.' || node.children[num] == null) {
      return;
    }
    node = node.children[num];
    if (node.word != null) {
      result.add(node.word);
      node.word = null;
    }
    board[i][j] = '.';
    if (i > 0) {
      this.dfs(board, i - 1, j, node, result);
    }
    if (j > 0) {
      this.dfs(board, i, j - 1, node, result);
    }
    if (i < board.length - 1) {
      this.dfs(board, i + 1, j, node, result);
    }
    if (j < board[0].length - 1) {
      this.dfs(board, i, j + 1, node, result);
    }
    board[i][j] = c;
  }

  private TrieNode initTrieNode(String[] words) {
    TrieNode root = new TrieNode();
    for (String word : words) {
      TrieNode node = root;
      for (char c : word.toCharArray()) {
        int num = c - 'a';
        if (node.children[num] == null) {
          node.children[num] = new TrieNode();
        }
        node = node.children[num];
      }
      node.word = word;
    }
    return root;
  }

}

class TrieNode {

  public String word;
  public TrieNode[] children;

  public TrieNode() {
    this.children = new TrieNode[26];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/572400235/){:target="_blank"}

# 설명
1. 주어진 2차원 배열 board를 이용하여 인접한 문자들의 조합이 주어진 배열 words에 있는 단어 중 만들 수 있는 단어들을 찾는 문제이다.

2. 문제 풀이에 필요한 TrieNode 클래스를 정의한다.
- word는 주어진 단어를 이용하여 TrieNode를 완성하고, 마지막 TrieNode에 해당 단어를 저장하기 위한 변수이다.
- children은 해당 단어까지의 문자열 이후의 문자열을 이어주기 위한 변수로, 객체 생성 시 다음 문자를 저장하기 위해 알파벳의 개수인 26 크기의 TrieNode 배열로 초기화 한다.

3. 주어진 단어들인 words를 이용하여 Trie를 완성한다.
- Trie를 만들기 위해 최상위 TrieNode인 root를 정의한다.
- 주어진 단어들인 words를 반복하여 TrieNode를 만들어준다.
  - 전역 변수인 root를 지역 변수인 node에 복사해준다.
    - 주어진 root를 점층적으로 내려가며 단어의 완성을 할 때, 기존 값들을 보호하기 위해서 node에 복사하여 node를 변경하며 수행하는 것이다.
  - 주어진 word를 한 문자씩 반복하여 node 아래로 문자열을 TrieNode에 연결시켜준다.
    - 주어진 word의 idx번째 문자에서 'a'를 빼 0(a) ~ 25(z))까지 숫자를 num에 넣어준다.
    - node.children의 num번째 TrieNode가 null인 경우, 하위 문자열을 이어주기 위해서 새 TrieNode를 넣어준다.
    - node에 node.children[num]을 넣어 이후 문자들을 이용하여 Trie를 완성한다.
  - 반복이 완료되면 마지막 TrieNode의 word에 해당 단어를 넣어준다.

4. 2차원 배열인 board를 반복하여 모든 위치에서 주어진 word를 만들 수 있는지를 검증하여 가능한 단어들만 result에 넣어준다.
- board[i][j]의 문자를 c, c - 'a'를 num 변수에 넣어준다.
- c가 '.'인 경우 해당 문자의 위치는 검증이 시작된 자리이고, node.children[num]이 null인 경우 주어진 문자에 존재하지 않으므로 수행을 중단한다.
- node에 node.children[num]을 넣어주고, node.word가 null이 아니면 주어진 words에 포함된 단어이므로 result에 넣어주고 node.word를 null로 변환하여 중복으로 들어가지 않도록 한다.
- board[i][j]를 '.'으로 바꾸어 해당 문자열 검증의 시작 위치임을 표시해준다.
- board[i][j]를 기준으로 상하좌우 네 방향으로 재귀 호출을 수행하여 문자열 검증을 진행한다.
- 검증이 완료된 이후 board[i][j]에 c를 넣어 원래 상태의 board로 복구한다.

5. 반복이 완료되면 주어진 배열인 words에 있는 단어들 중 주어진 2차원 배열 board를 이용하여 만들 수 있는 단어들만 추려낸 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WordSearchII.java){:target="_blank"}에서 확인 가능합니다.