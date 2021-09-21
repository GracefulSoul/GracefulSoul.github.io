---
title: "Leetcode Java Excel Sheet Column Number"
excerpt: "Leetcode Excel Sheet Column Number Java 풀이"
last_modified_at: 2021-09-21T18:00:00
header:
  image: /assets/images/leetcode/excel-sheet-column-number.png
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
[Link](https://leetcode.com/problems/excel-sheet-column-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int titleToNumber(String columnTitle) {
    int result = 0;
    for (int idx = 0; idx < columnTitle.length(); idx++) {
      result *= 26;
      result += columnTitle.charAt(idx) - 'A' + 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/558536318/){:target="_blank"}

# 설명
1. 지난 [Excel Sheet Column Title](excel-sheet-column-title)와 반대로, 주어진 엑셀 컬럼명인 columnTitle을 이용하여 정수형으로 바꾸는 문제이다.
- 'A'(1) ~ 'Z'(26)으로 구성되어 있으며, 복합 문자열 'AA'의 정수형 값은 27이다.

2. 주어진 엑셀 컬럼명인 columnTitle을 정수형을 바꾸어 넣기 위한 변수 result를 정의한다.

3. columnTitle의 각 문자를 반복하여 result에 컬럼명을 정수형으로 변환하여 합쳐준다.
- result의 값에 26을 곱하여 기존 자리의 값을 증가시켜준다.
  - 각 자리에 해당하는 문자열의 값에 $26^{(columnTitle.length - (idx + 1))}$을 곱해주는 것으로, 먼저 result에 26을 곱해준다.
  - 예를 들어, columnTitle이 'ABC'로 주어졌을 경우 $'A'(1) * 26^2 + 'B'(2) * 26^1 + 'C'(3) * 26^0 = 676 + 52 + 3 = 731$이 된다.
- result의 값에 idx번째 문자의 값을 더해준다.
  - 가져온 문자에 'A'의 ASCII 코드 값을 빼고 1을 더함으로써, 1번의 설명에 해당하는 1~26까지 값으로 변환해서 result에 더해주는 것이다.

4. 반복이 완료되면 columnTitle을 정수형으로 바꾸어 저장된 값을 담은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MajorityElement.java){:target="_blank"}에서 확인 가능합니다.