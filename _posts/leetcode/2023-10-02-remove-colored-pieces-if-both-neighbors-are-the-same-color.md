---
title: "Leetcode Java Remove Colored Pieces if Both Neighbors are the Same Color"
excerpt: "Leetcode Medium - 'Remove Colored Pieces if Both Neighbors are the Same Color' 문제 Java 풀이"
last_modified_at: 2023-10-02T10:05:00
header:
  image: /assets/images/leetcode/remove-colored-pieces-if-both-neighbors-are-the-same-color.png
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
[Link](https://leetcode.com/problems/remove-colored-pieces-if-both-neighbors-are-the-same-color){:target="_blank"}

# 코드
```java
class Solution {

  public boolean winnerOfGame(String colors) {
    char[] charArray = colors.toCharArray();
    int sum = 0;
    for (int i = 1; i < charArray.length - 1; i++) {
      if (charArray[i] == charArray[i - 1] && charArray[i] == charArray[i + 1]) {
        if (charArray[i] == 'A') {
          sum++;
        } else {
          sum--;
        }
      }
    }
    return sum > 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/remove-colored-pieces-if-both-neighbors-are-the-same-color/submissions/1064482780/){:target="_blank"}

# 설명
1. 'A'와 'B' 문자로 이루어진 colors를 이용하여 좌우 문자가 동일한 문자의 갯수가 'B'보다 'A'가 더 많은지 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 colors를 문자열로 변환하여 저장한 변수이다.
- sum은 좌우 문자가 동일한 'A' 문자의 갯수를 저장하기 위한 변수로, 0으로 초기화시켜준다.

3. 1부터 charArray의 길이보다 1 작은 값 미만까지 i를 증가시키며 아래를 반복한다.
- charArray[i]의 좌우 문자가 같은 경우, 해당 문자가 'A'면 sum을 증가 'B'면 sum을 감소시킨다.

4. sum이 0보다 큰지 검증한 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveColoredPiecesIfBothNeighborsAreTheSameColor.java){:target="_blank"}에서 확인 가능합니다.