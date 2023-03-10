---
title: "Leetcode Java Word Ladder"
excerpt: "Leetcode Word Ladder Java 풀이"
last_modified_at: 2021-08-16T14:40:00
header:
  image: /assets/images/leetcode/word-ladder.png
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
[Link](https://leetcode.com/problems/word-ladder/){:target="_blank"}

# 코드
```java
class Solution {

  public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    if (!wordList.contains(endWord)) {
      return 0;
    }
    Set<String> wordSet = new HashSet<>(wordList);
    Queue<String> queue = new LinkedList<>();
    queue.add(beginWord);
    int length = 1;
    while (!queue.isEmpty()) {
      int queueSize = queue.size();
      for (int i = 0; i < queueSize; i++) {
        char[] wordCharArr = queue.poll().toCharArray();
        for (int j = 0; j < wordCharArr.length; j++) {
          char temp = wordCharArr[j];
          for (char chr = 'a'; chr <= 'z'; chr++) {
            wordCharArr[j] = chr;
            String dest = new String(wordCharArr);
            if (wordSet.contains(dest)) {
              if (dest.equals(endWord)) {
                return length + 1;
              }
              queue.add(dest);
              wordSet.remove(dest);
            }
          }
          wordCharArr[j] = temp;
        }
      }
      length++;
    }
    return 0;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/539226086/){:target="_blank"}

# 설명
1. 주어진 문자열 beginWord를 endWord로 변환하기 위한 가장 짧은 순서를 배열 wordList에서 찾아서 변환 횟수를 구하는 문제이다.

2. wordList에 endWord가 존재하지 않으면, 변환이 불가능하므로 0을 주어진 문제의 결과로 반환한다.

3. 문제 풀이에 필요한 변수들을 정의한다.
- wordSet은 주어진 List인 wordList의 동적으로 확인하여 제거하기 위해 변환하여 정의한다.
- queue는 변환되는 단어를 임시 저장하기 위해 LinkedList로 정의하고, 변환하기 위한 처음 단어로 beginWord를 넣어 초기화한다.
- length는 변환 횟수를 저장하기 위한 변수로 1로 초기화한다.

4. 변환 시킬 단어를 저장한 queue가 비어있지 않을 때 까지 반복하여 변환 횟수를 계산한다.
- queue는 단어를 임시 저장시키는 용도로, 변동이 가능하므로 queue에 담긴 단어의 개수를 임시로 queueSize 변수에 넣어 저장한다.
- queueSize만큼 반복하여 변환 횟수를 계산한다.

5. queue에 담긴 단어를 꺼내와 문자의 배열로 정의하고, 해당 단어의 길이만큼 반복을 수행한다.

6. wordCharArr[j]의 값을 temp 변수에 넣고, a부터 z까지 반복하여 wordCharArr[j]에 넣어 wordSet에 해당 단어가 존재하는지 확인한다.
- 변환된 값이 endWord와 같다면 해당 변환에서 endWord로 변환이 완료 된 것이므로, 변환 횟수를 저장한 length에 1을 더하여 주어진 문제의 결과로 반환한다.
- 변환된 값이 존재하는 경우, queue에 해당 단어를 넣고, wordSet에 해당 단어를 제거한다.

7. 반복이 완료되면 wordCharArr[j]에 다시 temp를 넣어준다.

8. queueSize만큼 반복이 완료되면 length를 증가시켜 변환 횟수를 증가시킨다.

9. 위의 절차들이 완료되면 변환이 불가능하므로, 0을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WordLadder.java){:target="_blank"}에서 확인 가능합니다.