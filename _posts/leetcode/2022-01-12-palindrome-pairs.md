---
title: "Leetcode Java Palindrome Pairs"
excerpt: "Leetcode - 'Palindrome Pairs' 문제 Java 풀이"
last_modified_at: 2022-01-12T12:00:00
header:
  image: /assets/images/leetcode/palindrome-pairs.png
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
[Link](https://leetcode.com/problems/palindrome-pairs/){:target="_blank"}

# 코드
```java
class Solution {

  private TrieNode root = new TrieNode();

  public List<List<Integer>> palindromePairs(String[] words) {
    List<List<Integer>> result = new ArrayList<>();
    int length = words.length;
    for (int idx = 0; idx < length; idx++) {
      this.add(words[idx], idx);
    }
    for (int idx = 0; idx < length; idx++) {
      this.search(result, words[idx], idx);
    }
    return result;
  }

  private boolean isPalindrome(char[] charArray, int start, int end) {
    while (start < end) {
      if (charArray[start++] != charArray[end--]) {
        return false;
      }
    }
    return true;
  }

  private void add(String word, int wordIndex) {
    TrieNode temp = root;
    char[] charArray = word.toCharArray();
    for (int idx = charArray.length - 1; idx >= 0; idx--) {
      int num = charArray[idx] - 'a';
      if (this.isPalindrome(charArray, 0, idx)) {
        temp.palindromeWordIndexes.add(wordIndex);
      }
      if (temp.children[num] == null) {
        temp.children[num] = new TrieNode();
      }
      temp = temp.children[num];
    }
    temp.wordIndex = wordIndex;
  }

  private void search(List<List<Integer>> result, String word, int wordIndex) {
    TrieNode temp = root;
    char[] charArray = word.toCharArray();
    for (int idx = 0; idx < charArray.length; idx++) {
      int num = charArray[idx] - 'a';
      if (temp.wordIndex != -1 && this.isPalindrome(charArray, idx, charArray.length - 1)) {
        result.add(Arrays.asList(wordIndex, temp.wordIndex));
      }
      if (temp.children[num] == null) {
        return;
      }
      temp = temp.children[num];
    }
    if (temp.wordIndex != -1 && temp.wordIndex != wordIndex) {
      result.add(Arrays.asList(wordIndex, temp.wordIndex));
    }
    for (int palindromeWordIndex : temp.palindromeWordIndexes) {
      result.add(Arrays.asList(wordIndex, palindromeWordIndex));
    }
  }

}

class TrieNode {

  public int wordIndex;
  public List<Integer> palindromeWordIndexes;
  public TrieNode[] children;

  public TrieNode() {
    this.wordIndex = -1;
    this.palindromeWordIndexes = new ArrayList<>();
    this.children = new TrieNode[26];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/618055953/){:target="_blank"}

# 설명
1. 앞뒤로 읽어도 같은 문자열(이하 회문)을 만들 수 있는 주어진 문자열 배열인 words 내 두 단어의 조합의 인덱스를 반환하는 문제이다.

2. 문제 풀이에 필요한 TrieNode 클래스를 정의한다.
- wordIndex는 해당 단어의 words 내 위치인 인덱스를 저장하는 변수이다.
- palindromeWordIndexes는 회문이 되는 words 내 위치인 인덱스를 저장할 변수이다.
- children은 해당 단어까지의 문자열 이후의 문자열을 이어주기 위한 변수로, 객체 생성 시 다음 문자를 저장하기 위해 알파벳의 개수인 26 크기의 TrieNode 배열로 초기화 한다.

3. 문제 풀이에 필요한 전역 변수를 정의한다.
- root는 주어진 words를 이용하여 [Trie](https://en.wikipedia.org/wiki/Trie){:target="_blank"}를 완성하기 위한 변수이다.

4. 문제 풀이에 필요한 isPalindrome(char[] charArray, int start, int end) 메서드를 완성한다.
- start가 end보다 작을 때 까지 반복하여 charArray의 start번째 값과 end번째 값이 같지 않으면 회문이 아니므로 false를 반환하고, start를 증가시키고 end를 감소시키고 반복을 계속 진행한다.
- 반복이 완료되면 charArray가 회문으로 구성되어 있으므로 true를 반환한다.

5. 문제 풀이에 필요한 add(String word, int wordIndex) 메서드를 완성한다.
- root를 지역 변수 temp에 넣어주고, word를 charArray에 문자의 배열로 변환하여 넣어준다.
- charArray를 역순으로 반복하여 Trie를 완성한다.
  - num에 charArray의 idx번째 문자와 'a'의 차이인 영소문자의 순서값으로 변환시킨다.
  - charArray의 0부터 idx번째 값까지 4번의 isPalindrome 메서드를 활용하여 검증하고, 회문이 되면 temp의 palindromeWordIndexes에 wordIndex를 넣어준다.
  - temp.children의 num번째 TrieNode가 null인 경우, 새 TrieNode를 생성하여 넣어준다.
  - temp에 temp.children의 num번째 TrieNode를 넣고 반복을 계속 진행한다.
- 반복이 완료되면 temp.wordIndex에 wordIndex를 넣어준다.

6. 문제 풀이에 필요한 search(List<List<Integer>> result, String word, int wordIndex) 메서드를 완성한다.
- root를 지역 변수 temp에 넣어주고, word를 charArray에 문자의 배열로 변환하여 넣어준다.
- charArray를 처음부터 끝까지 반복하여 검색을 수행한다.
  - num에 charArray의 idx번째 문자와 'a'의 차이인 영소문자의 순서값으로 변환시킨다.
  - temp.wordIndex가 -1이 아니면서 charArray의 idx번째 값부터 끝까지 회문이 되는 경우, result에 wordIndex와 temp.wordIndex를 List로 묶어 넣어준다.
  - temp.children의 num번째 값이 null인 경우, 문자열의 끝이므로 검색을 중단한다.
  - temp에 temp.children의 num번째 값을 넣어주고 반복을 계속 수행한다.
- temp.wordIndex가 -1이 아니면서 temp.wordIndex가 wordIndex가 아닌 경우 전체가 회문이 되는 경우이므로, result에 wordIndex와 temp.wordIndex를 List로 묶어 넣어준다.
- temp의 palindromeWordIndexes를 반복하여 회문이 되는 모든 조합을 result에 wordIndex와 palindromeWordIndex를 List로 묶어 넣어준다.

7. 문제 풀이에 수행되는 palindromePairs(String[] words) 메서드를 완성한다.
- 문제 풀이에 필요한 변수를 정의한다.
  - result는 회문이 되는 조합을 넣을 List로, 새 ArrayList로 초기화 하여 정의한다.
  - length는 words의 길이를 저장할 변수로, words.length를 넣어 정의한다.
- 0부터 length까지 idx를 증가시키며, 5번에서 생성한 add(String word, int wordIndex) 메서드를 이용하여 words의 각 문자들을 TrieNode에 넣어준다.
- 0부터 length까지 idx를 증가시키며, 6번에서 생성한 search(List<List<Integer>> result, String word, int wordIndex) 메서드를 이용하여 result에 회문이 되는 모든 조합을 넣어준다.
- 위의 수행이 완료되면 회문이 되는 모든 두 문자의 조합을 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PalindromePairs.java){:target="_blank"}에서 확인 가능합니다.