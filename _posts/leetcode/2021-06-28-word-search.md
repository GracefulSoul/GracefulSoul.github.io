---
title: "Leetcode Java Word Search"
excerpt: "Leetcode Word Search Java 풀이"
last_modified_at: 2021-06-28T13:00:00
header:
  image: /assets/images/leetcode/word-search.png
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
[Link](https://leetcode.com/problems/word-search/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean exist(char[][] board, String word) {
    char[] charArray = word.toCharArray();
    for (int row = 0; row < board.length; row++) {
      for (int col = 0; col < board[row].length; col++) {
        if (this.check(board, row, col, charArray, 0)) {
          return true;
        }
      }
    }
    return false;
  }

  private boolean check(char[][] board, int row, int col, char[] charArray, int idx) {
    if (idx == charArray.length) {
      return true;
    } else if (row < 0 || col < 0 || row == board.length || col == board[row].length
        || board[row][col] != charArray[idx]) {
      return false;
    } else {
      board[row][col] = 0;
      boolean exist = this.check(board, row, col + 1, charArray, idx + 1)
          || this.check(board, row + 1, col, charArray, idx + 1)
          || this.check(board, row, col - 1, charArray, idx + 1)
          || this.check(board, row - 1, col, charArray, idx + 1);
      board[row][col] = charArray[idx];
      return exist;
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/514222856/){:target="_blank"}

# 설명
1. 주어진 2차원 배열 board의 값들을 이어 주어진 문자열 word를 만들 수 있는지 검증하는 문제이다.

2. 배열을 탐색하기 전에 주어진 문자열 word를 문자의 배열로 변환한다.

3. 배열을 반복하여 주어진 문자열 word를 만들 수 있으면 주어진 문제의 결과로 true를 반환한다.
- 문자열 검증에 포인터로 사용되는 idx가 주어진 문자열 word의 길이와 같으면, true를 반환한다.
- 배열의 탐색에 사용되는 row와 col이 0보다 작거나 배열크기보다 큰 경우와 board[row][col]의 값이 charArray[idx]의 값과 동일하지 않으면, false를 반환한다.
- 그 외의 경우 현재 위치의 값을 0으로 초기화 하여 사용된 값을 표시하고 상하좌우의 값들을 이용하여 다음 문자가 존재하는지를 검증하고 다시 현재 위치의 값을 복원 후 검증한 값을 반환한다.

4. 반복이 완료되면 주어진 2차원 배열 board의 값으로 문자열 word를 만들지 못한다는 의미이므로, 주어진 문제의 결과로 false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WordSearch.java){:target="_blank"}에서 확인 가능합니다.