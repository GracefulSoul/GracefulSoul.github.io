---
title: "Leetcode Java Rotating the Box"
excerpt: "Leetcode - 'Rotating the Box' 문제 Java 풀이"
last_modified_at: 2024-11-23T10:00:00
header:
  image: /assets/images/leetcode/rotating-the-box.png
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
[Link](https://leetcode.com/problems/rotating-the-box/){:target="_blank"}

# 코드
```java
class Solution {

  public char[][] rotateTheBox(char[][] box) {
    int row = box.length;
    int col = box[0].length;
    char[][] result = new char[col][row];
    for (int i = 0; i < row; i++) {
      for (int j = col - 1, k = col - 1; j >= 0; j--) {
        result[j][row - i - 1] = '.';
        if (box[i][j] != '.') {
          if (box[i][j] == '*') {
            k = j;
          }
          result[k--][row - i - 1] = box[i][j];
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/rotating-the-box/submissions/1460398717/){:target="_blank"}

# 설명
1. box를 우측으로 90도 기울인 배열을 반환하는 문제이다.
- box내 값들 중 '#'는 돌, '*'는 장애물, '.'는 빈 공간을 의미한다.
- box를 우측으로 기울였을 때 돌은 장애물을 만나기 전까지 아래로 이동할 수 있다.

2. 문제 풀이에 필요한 변수를 정의한다.
- row와 col은 bot의 행과 열 갯수를 저장한 변수이다.
- result는 결과를 저장할 변수로, 행과 열의 길이를 반대로한 $col \times row$ 크기의 문자 배열로 초기화한다.

3. 0부터 row 미만까지 i를 증가시키고, j와 k를 $col - 1$로 초기화 후 j가 0 이상일 때 까지 감소시키면서 아래를 반복한다.
- result[j][$row - i - 1$]의 자리에 '.'를 넣어 빈공간으로 초기화한다.
- box[i][j]의 값이 '.'이 아닌 경우, 아래를 수행한다.
  - box[i][j]의 값이 '*'인 장애물인 경우, k에 j를 넣어 result에 넣을 위치인 k를 이동한다.
- result[k][$row - i - 1$]의 자리에 box[i][j]의 값을 그대로 넣어주고 k를 감소시킨다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RotatingTheBox.java){:target="_blank"}에서 확인 가능합니다.