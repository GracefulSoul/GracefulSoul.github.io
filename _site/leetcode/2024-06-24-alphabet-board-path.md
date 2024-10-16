---
title: "Leetcode Java Alphabet Board Path"
excerpt: "Leetcode Alphabet Board Path Java"
last_modified_at: 2024-06-24T18:10:00
header:
  image: /assets/images/leetcode/alphabet-board-path.png
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
[Link](https://leetcode.com/problems/alphabet-board-path/){:target="_blank"}

# 코드
```java
class Solution {

  public String alphabetBoardPath(String target) {
    int x = 0;
    int y = 0;
    StringBuilder sb = new StringBuilder();
    for (char c : target.toCharArray()) {
      int x1 = (c - 'a') / 5;
      int y1 = (c - 'a') % 5;
      while (x1 < x) {
        x--;
        sb.append('U');
      }
      while (y1 > y) {
        y++;
        sb.append('R');
      }
      while (y1 < y) {
        y--;
        sb.append('L');
      }
      while (x1 > x) {
        x++;
        sb.append('D');
      }
      sb.append('!');
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/alphabet-board-path/submissions/1298562896/){:target="_blank"}

# 설명
1. 영문자 구성인 board의 (0, 0)위치에서 시작해서 target 문자열을 만들기 위한 과정을 순차적으로 문자열로 만들어 반환하는 문제이다.
- board는 ["abcde", "fghij", "klmno", "pqrst", "uvwxy", "z"]로 구성되어있다.
- 'U'는 위로, 'D'는 아래로, 'L'은 좌측으로, 'R'은 우측으로 이동하는 것을 의미한다.
- '!'는 이동한 위치의 문자가 target 문자열 생성에 필요한 값임을 의미한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- x와 y는 현재 위치값을 의미하며, 처음 위치인 0으로 둘 다 초기화한다.
- sb는 이동 경로에 대한 문자를 동적으로 생성하기 위한 변수로, StringBuilder로 초기화한다.

3. target의 각 문자들을 순서대로 c에 넣어 아래를 수행한다.
- x1과 y1은 c의 위치를 저장할 변수로, 문자의 순서인 $c - 'a'$ 값을 한 행의 문자 갯수인 5로 나눈 몫을 x1에 나머지를 y1에 넣어준다.
- x1이 x보다 작을 때 까지 x를 감소시키고 sb에 'U'문자를 이어 위로 이동했음을 표기한다.
- y1이 y보다 클 때 까지 y를 증가시키고 sb에 'R'문자를 이어 우측으로 이동했음을 표기한다.
- y1이 y보다 작을 때 까지 y를 감소시키고 sb에 'L'문자를 이어 좌측으로 이동했음을 표기한다.
- x1이 x보다 클 때 까지 x를 증가시키며 sb에 'D'문자를 이어 아래로 이동했음을 표기한다.
- 목표 위치로 이동이 완료되면 sb에 '!' 문자를 이어 목표 문자로 이동했음을 표기한다.

4. 반복이 완료되면 target 문자열을 만들기 위한 과정이 저장된 sb를 문자열로 변환하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumOfAbsoluteValueExpression.java){:target="_blank"}에서 확인 가능합니다.