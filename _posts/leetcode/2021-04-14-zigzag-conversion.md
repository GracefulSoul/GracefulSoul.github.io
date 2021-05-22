---
title: "Leetcode Java ZigZag Conversion"
excerpt: "Leetcode ZigZag Conversion Java 풀이"
last_modified_at: 2021-04-14T20:40:00
header:
  image: /assets/images/leetcode/zigzag-conversion.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - Java

toc: true
toc_ads: true
toc_sticky: true
---
# 문제
[Link](https://leetcode.com/problems/zigzag-conversion/){:target="_blank"}

# 코드
```java
class Solution {

  public String convert(String s, int numRows) {
    if (numRows == 1) {
      return s;
    }
    char[] c = s.toCharArray();
    StringBuilder[] sbArr = initStringBuilderArray(numRows);
    int sign = 1;
    int i = 0;
    for (int idx = 0; idx < c.length; idx++) {
      sbArr[i].append(c[idx]);
      if (idx != 0 && idx % (numRows - 1) == 0) {
        sign *= (-1);
      }
      i += sign;
    }
    return getResult(sbArr);
  }

  private StringBuilder[] initStringBuilderArray(int numRows) {
    StringBuilder[] sbArr = new StringBuilder[numRows];
    for (int idx = 0; idx < sbArr.length; idx++) {
      sbArr[idx] = new StringBuilder();
    }
    return sbArr;
  }

  private String getResult(StringBuilder[] sbArr) {
    for (int idx = 1; idx < sbArr.length; idx++) {
      sbArr[0].append(sbArr[idx]);
    }
    return sbArr[0].toString();
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/480333369/){:target="_blank"}

# 설명
1. 주어진 행의 수인 변수 numRows가 1이면 주어진 문자열 그대로이므로, 주어진 문제의 결과로 반환한다.

2. 주어진 문자열 s를 문자 배열 c에 저장하고, 주어진 행의 수인 변수 numRows를 이용하여 StringBuilder 배열인 sbArr을 만든다.
- StringBuilder 배열은 행의 숫자인 numRows 크기로 만든다.
- 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.

3. 방향을 나탄는 변수 sign과 지그재그로 표현하기 위한 최대 꼭짓점인 변수 i를 선언한다.
- 변수 sign은 양수/음수에 따라서 아래로 내려갔다가 다시 위로 올라오기 위해 사용한다.
- 변수 i는 지그재그의 꼭짓점(가장 아랫부분의 길이)까지 반복하기 위해사용한다.

4. 문자 배열 c의 크기만큼 반복을 통해 주어진 결과를 생성한다.
- sbArr의 i 번째 index에 c\[idx\] 값을 주입한다.
- 만일 idx가 0이 아니거나, idx를 numRows - 1로 나눈 나머지 값이 0인 경우 sign에 -1을 곱하여 방향을 전환한다.
- idx가 0인 경우, 무슨 값으로 나누더라도 결과는 0이므로 이 경우는 제외하도록 한다.
- idx를 numRows - 1로 나눈 값이 0인 경우, 맨 위에서 c\[idx\] 값을 주입한 이후 위치가 지그재그의 모서리(시작과 끝) 높이이므로 방향을 바꾸어 준다.

5. sbArr 값을 하나의 문자열로 합쳐서 주어진 문제의 결과로 반환한다.
- sbArr[0]의 값에 0 이후 index 배열의 값을 append 시켜 sbArr[0].toString()을 통해 간단히 하나의 문자열로 생성하였다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ZigZagConversion.java){:target="_blank"}에서 확인 가능합니다.