---
title: "Leetcode Java Implement Magic Dictionary"
excerpt: "Leetcode Implement Magic Dictionary Java"
last_modified_at: 2022-09-29T19:40:00
header:
  image: /assets/images/leetcode/implement-magic-dictionary.png
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
[Link](https://leetcode.com/problems/implement-magic-dictionary){:target="_blank"}

# 코드
```java
class MagicDictionary {

  private Map<Integer, List<String>> map;

  public MagicDictionary() {
    this.map = new HashMap<>();
  }

  public void buildDict(String[] dictionary) {
    for (String word : dictionary) {
      List<String> words = this.map.get(word.length());
      if (words == null) {
        words = new ArrayList<>();
        this.map.put(word.length(), words);
      }
      words.add(word);
    }
  }

  public boolean search(String searchWord) {
    List<String> words = this.map.get(searchWord.length());
    if (words != null) {
      for (String word : words) {
        int count = 0;
        for (int idx = 0; idx < word.length(); idx++) {
          if (word.charAt(idx) != searchWord.charAt(idx)) {
            count++;
            if (count > 1) {
              break;
            }
          }
        }
        if (count == 1) {
          return true;
        }
      }
    }
    return false;
  }

}

/**
 * Your MagicDictionary object will be instantiated and called as such:
 * MagicDictionary obj = new MagicDictionary();
 * obj.buildDict(dictionary);
 * boolean param_2 = obj.search(searchWord);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/811281531/){:target="_blank"}

# 설명
1. 문자열을 입력받아 데이터 구조 내 단어에서 검색 단어의 한 문자만 수정해서 구성할 수 있는지 검색하는 기능을 수행하는 MagicDictionary 클래스를 완성하는 문제이다.
- 생성자인 MagicDictionary()는 객체를 초기화한다.
- 메서드인 buildDict(String[] dictionary)은 데이터 구조 내 dictionary를 넣어주는 역할을 수행한다.
- 메서드인 search(String searchWord)는 데이터 구조 내 문자들 중 searchWord의 한 문자만 변경한 값과 동일한지 검증한 결과를 반환하는 역할을 수행한다.

2. 문제 풀이에 필요한 전역 변수를 정의한다.
- map은 문자열의 길이 별 문자들을 저장할 변수이다.

3. 생성자인 MagicDictionary()를 정의한다.
- map을 HashMap으로 초기화 한다.

4. 메서드인 buildDict(String[] dictionary)을 정의한다.
- dictionary의 모든 단어를 word에 순차적으로 넣어 아래를 반복한다.
  - words에 map 내 word의 길이가 키인 값을 가져온다.
  - words가 없는 경우, words를 새 ArrayList로 초기화하고 map에 words 길이의 값에 words를 넣어준다.
  - words에 word를 넣고 반복을 계속 수행한다.

5. 메서드인 search(String searchWord)를 정의한다.
- words에 map 내 searchWord의 길이가 키인 값을 가져온다.
- words가 null이 아니면 words의 모든 단어를 word에 순차적으로 넣어 아래를 반복한다.
  - count는 변경된 문자의 갯수를 넣을 변수로, 0으로 초기화한다.
  - word와 searchWord를 비교하여 변경할 단어인 count가 1인 경우, true를 반환한다.
- 반복이 완료되면 한 문자만 변경해서 동일하게 구성할 단어를 찾지 못했으므로, false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ImplementMagicDictionary.java){:target="_blank"}에서 확인 가능합니다.