---
title: "Leetcode Java Construct Smallest Number From DI String"
excerpt: "Leetcode - 'Construct Smallest Number From DI String' 문제 Java 풀이"
last_modified_at: 2025-02-18T18:55:00
header:
  image: /assets/images/leetcode/construct-smallest-number-from-di-string.png
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
[Link](https://leetcode.com/problems/construct-smallest-number-from-di-string/){:target="_blank"}

# 코드
```java
class Solution {

  public String smallestNumber(String pattern) {
    StringBuilder sb = new StringBuilder();
    int length = pattern.length();
    int[] stack = new int[length + 1];
    int index = 0;
    for (int i = 0; i <= length; i++) {
      stack[index++] = i + 1;
      if (i == length || pattern.charAt(i) == 'I') {
        while (index > 0) {
          sb.append(stack[--index]);
        }
      }
    }
    return sb.toString();
  }

}
```

# 결과
[Link](https://leetcode.com/problems/construct-smallest-number-from-di-string/submissions/1547243168/){:target="_blank"}

# 설명
1. pattern의 값을 사전적으로 가장 작은 값인 num을 만들어 반환하는 문제이다.
- num은 '1'에서 '9'까지로 구성된 숫자이다.
- pattern[i] 값이 'I'면 증가하는 값을 의미하며, num[i] < num[$i + 1$]를 만족한다.
- pattern[i] 값이 'D'면 감소하는 값을 의미하며, num[i] > num[$i + 1$]를 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- sb는 num을 만들기 위한 변수로, 동적 문자열 생성을 위한 StringBuilder로 초기화한다.
- length는 pattern의 길이를 저장한 변수이다.
- stack은 각 숫자를 위치 별 저장하기 위한 변수로, $length + 1$ 크기의 정수 배열로 초기화한다.
- index는 stack의 위치를 저장할 변수로, 0으로 초기화한다.

3. 0부터 length 이하까지 i를 증가시키며 아래를 반복한다.
- stack[index]의 값에 $i + 1$을 넣어주고 index를 증가시킨다.
- i가 마지막 위치인 length이거나 pattern의 i번째 문자가 'I'인 경우, index가 0보다 클 때까지 index를 감소시킨 후 sb에 stack[index] 값을 넣어 num 문자열을 만들어준다.

4. 반복이 완료되면 완성된 문자열 sb를 문자열로 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConstructSmallestNumberFromDIString.java){:target="_blank"}에서 확인 가능합니다.