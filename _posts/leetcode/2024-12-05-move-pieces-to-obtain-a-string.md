---
title: "Leetcode Java Move Pieces to Obtain a String"
excerpt: "Leetcode - 'Move Pieces to Obtain a String' 문제 Java 풀이"
last_modified_at: 2024-12-05T16:20:00
header:
  image: /assets/images/leetcode/move-pieces-to-obtain-a-string.png
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
[Link](https://leetcode.com/problems/move-pieces-to-obtain-a-string/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canChange(String start, String target) {
    char[] startCharArray = start.toCharArray();
    char[] targetCharArray = target.toCharArray();
    int length = targetCharArray.length;
    int i = 0;
    int j = 0;
    while (i <= length && j <= length) {
      while (i < length && targetCharArray[i] == '_') {
        i++;
      }
      while (j < length && startCharArray[j] == '_') {
        j++;
      }
      if (i == length || j == length) {
        return i == length && j == length;
      }
      if (targetCharArray[i] != startCharArray[j]) {
        return false;
      }
      if (targetCharArray[i] == 'L') {
        if (j < i) {
          return false;
        }
      } else {
        if (i < j) {
          return false;
        }
      }
      i++;
      j++;
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/move-pieces-to-obtain-a-string/submissions/1470800610/){:target="_blank"}

# 설명
1. 'L', 'R', '_' 문자로 이루어진 문자열 start를 target으로 변경 가능한지 검증하는 문제이다.
- 문자 'L', 'R'은 왼쪽과 오른쪽 방향을 뜻하며, 각 방향에 빈 공간인 '_' 문자가 존재해야 해당 방향으로 이동 가능하다.

2. 문제 풀이에 필요한 변수를 정의한다.
- startCharArray와 targetCharArray는 start와 target을 문자 배열로 변환한 변수이다.
- length는 target의 길이를 저장한 변수이다.
- i와 j는 target과 start의 위치를 저장할 변수로, 둘 다 0으로 초기화한다.

3. i와 j가 length 이하일 때 까지 아래를 반복한다.
- i가 length 미만이면서 targetCharArray[i] 문자가 '_'인 이동 가능할 때 까지 i를 증가시켜 이동 가능한 마지막 위치로 이동시킨다.
- j가 length 미만이면서 startCharArray[j] 문자가 '_'인 이동 가능할 때 까지 j를 증가시켜 이동 가능한 마지막 위치로 이동시킨다.
- i 혹은 j가 length에 도달하는 경우, i와 j가 마지막 위치인지 여부를 주어진 문제의 결과로 반환한다.
- targetCharArray[i] 문자와 startCharArray[j] 문자가 다른 변경이 불가능한 경우, false를 주어진 문제의 결과로 반환한다.
- targetCharArray[i] 문자가 'L'이면서 j가 i 미만인 변환이 불가능한 경우, false를 주어진 문제의 결과로 반환한다.
- targetCharArray[i] 문자가 'R'이면서 i가 j 미만인 변환이 불가능한 경우, false를 주어진 문제의 결과로 반환한다.
- i와 j를 증가시켜 다음 위치로 이동시킨다.

4. 반복이 완료되어 변환이 가능한 경우, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MovePiecesToObtainAString.java){:target="_blank"}에서 확인 가능합니다.