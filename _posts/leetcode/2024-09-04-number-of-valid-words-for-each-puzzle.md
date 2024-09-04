---
title: "Leetcode Java Number of Valid Words for Each Puzzle"
excerpt: "Leetcode Number of Valid Words for Each Puzzle Java"
last_modified_at: 2024-09-04T18:10:00
header:
  image: /assets/images/leetcode/number-of-valid-words-for-each-puzzle.png
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
[Link](https://leetcode.com/problems/number-of-valid-words-for-each-puzzle/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Integer> findNumOfValidWords(String[] words, String[] puzzles) {
    Map<Integer, Integer> map = new HashMap<>();
    for (String word : words) {
      int mask = 0;
      for (char c : word.toCharArray()) {
        mask |= 1 << (c - 'a');
      }
      map.put(mask, map.getOrDefault(mask, 0) + 1);
    }
    List<Integer> result = new ArrayList<>();
    for (String puzzle : puzzles) {
      int mask = 0;
      for (char c : puzzle.toCharArray()) {
        mask |= 1 << (c - 'a');
      }
      int count = 0;
      int i = puzzle.charAt(0) - 'a';
      for (int j = mask; j > 0; j = (j - 1) & mask) {
        if ((j >> i & 1) == 1) {
          count += map.getOrDefault(j, 0);
        }
      }
      result.add(count);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-valid-words-for-each-puzzle/submissions/1378615107/){:target="_blank"}

# 설명
1. puzzles 배열 내 아래의 규칙을 만족하는 words의 갯수를 계산하는 문제이다.
- 이하부터 puzzles의 임의 문자열은 puzzle, words의 임의 문자열은 word로 한다.
- puzzle의 첫 문자은 word 문자열 내 존재해야 한다.
- puzzle의 각 문자들로 word 문자열을 만들 수 있어야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- map은 문자열을 만들 수 있는 비트의 갯수를 저장할 변수로, HashMap으로 초기화하여 words의 각 값을 bit 숫자열로 변환하여 갯수를 계산해 비트 별 갯수를 넣어준다.
- result는 puzzle로 주어진 조건을 만족하는 word의 갯수를 넣어줄 변수로, ArrayList로 초기화한다.

3. puzzles의 각 값을 순차적으로 puzzle에 넣어 아래를 수행한다.
- 만족하는 갯수 계산에 필요한 변수를 정의한다.
  - mask는 puzzle를 bit 숫자열로 변환한 변수이다.
  - count는 만족하는 word의 갯수를 계산하기 위한 변수로, 0으로 초기화한다.
  - i는 puzzle의 첫 문자 위치를 저장한 변수이다.
- mask부터 0 초과까지 j에 $j - 1$과 mask의 AND(&) 비트 연산을 수행한 결과를 넣어가며 아래를 반복한다.
  - i를 j번 우측으로 이동한 비트와 1의 AND(&) 비트 연산을 수행한 결과가 1인 경우, count에 map의 j번째 값을 더해준다. 값이 없으면 0을 더해준다.
- result에 count를 넣어 갯수를 저장해준다.

4. 반복이 완료되면 각자 만족하는 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfValidWordsForEachPuzzle.java){:target="_blank"}에서 확인 가능합니다.