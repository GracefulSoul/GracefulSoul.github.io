---
title: "Leetcode Java Excel Sheet Column Title"
excerpt: "Leetcode Excel Sheet Column Title Java 풀이"
last_modified_at: 2021-09-19T11:00:00
header:
  image: /assets/images/leetcode/excel-sheet-column-title.png
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
[Link](https://leetcode.com/problems/excel-sheet-column-title/){:target="_blank"}

# 코드
```java
class Solution {

  public String convertToTitle(int columnNumber) {
    StringBuilder result = new StringBuilder();
    while (columnNumber > 0) {
      result.append((char) ('A' + (--columnNumber % 26)));
      columnNumber /= 26;
    }
    if (result.length() > 1) {
      result.reverse();
    }
    return result.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/557236474/){:target="_blank"}

# 설명
1. 주어진 정수 columnNumber를 이용하여 엑셀의 컬럼명을 가져오는 문제이다.

2. 결과를 동적으로 생성하기 위해 StringBuilder인 result를 정의한다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

3. columnNumber가 0보다 클 때까지 반복하여 result에 엑셀 컬럼명을 넣는다.
- result에 $'A' + (--columnNumber % 26)$의 값을 문자로 변환하여 넣어준다.
  - 영어 대문자는 총 26개가 존재하며, 'A' 문자 기준으로 'Z'가 되기 위해서는 $'A' + 25$의 ASCII 코드 값이 되어야 한다.
  - 그렇기 때문에 'A'가 되기위해서는 columnNumber를 1을 뺀 후 26을 나눈 나머지 값을 이용하여 'A'문자의 ASCII 코드 값을 합치는 것이다.
  - 간단한 예를 들어 columnNumber가 1인 경우, 엑셀 필드명이 'A'로 반환되어야 하므로 $'A'(65) + 1$의 결과는 'B'(66)이 되버리기 때문에 1을 빼주는 것이다.
- columnNumber에 26을 나눈 값을 다시 넣어주고 반복을 계속 수행한다.

4. result에 들어간 문자가 1개 초과인 경우 result.reverse()를 통해 앞뒤를 반전시켜준다.
- StringBuilder의 append() method는 Stack처럼 넣은 순서대로 들어가기 때문에 2개 이상인 경우 앞뒤를 반전시켜주어야 원하는 필드 명이 완성된다.
- StringBuilder의 insert() method를 사용하면 첫 자리에 후입 문자가 들어갈 수 있지만 매 문자의 삽입 시, 순서의 변경을 위한 메모리가 낭비되므로 append()와 reverse()를 활용한다.

5. 완성된 엑셀의 컬럼명을 저장한 result를 문자열로 변환하여 주어진 문제의 결과로 반환한다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ExcelSheetColumnTitle.java){:target="_blank"}에서 확인 가능합니다.