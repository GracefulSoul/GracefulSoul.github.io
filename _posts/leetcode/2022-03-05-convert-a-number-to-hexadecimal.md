---
title: "Leetcode Java Convert a Number to Hexadecimal"
excerpt: "Leetcode - 'Convert a Number to Hexadecimal' 문제 Java 풀이"
last_modified_at: 2022-03-05T10:00:00
header:
  image: /assets/images/leetcode/convert-a-number-to-hexadecimal.png
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
[Link](https://leetcode.com/problems/convert-a-number-to-hexadecimal/){:target="_blank"}

# 코드
```java
class Solution {

  public String toHex(int num) {
    if (num == 0) {
      return "0";
    } else {
      StringBuilder sb = new StringBuilder();
      while (num != 0) {
        int n = num & 0xf;
        n += n < 0xa ? '0' : 'a' - 10;
        sb.append((char) n);
        num >>>= 4;
      }
      return sb.reverse().toString();
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/653479976/){:target="_blank"}

# 설명
1. 주어진 정수 num을 이용하여 16진수 표현 문자열을 반환하는 문제이다.
- 답변 문자열의 모든 문자는 소문자이고, num이 0인 경우를 제외하고 문자열 내 0을 제외하고 작성한다.

2. num이 0인 경우, "0"을 주어진 문제의 결과로 반환한다.

3. num이 0이 아닌 경우, 아래를 수행한다.
- 16진수 표현을 저장할 sb를 StringBuilder로 초기화한다.
  - 동적 문자열의 생성시, 효율적인 메모리 사용을 위해 [StringBuilder](https://docs.oracle.com/javase/tutorial/java/data/buffers.html){:target="_blank"}를 사용한다.
- num이 0이 아닐 때 까지 아래를 반복하여 sb에 값을 넣어준다.
  - n에 num과 0xf(15)의 AND(&) 비트 연산 수행 결과를 넣어준다.
  - n에 n이 0xa(10)보다 작은 경우 0, 같거나 큰 경우 $'a' - 10$을 더해준다.
  - sb에 n을 문자열로 변환한 값을 넣아주고, num의 비트를 우측으로 4칸 이동시킨다.
- 16진수 표현 문자열을 역순으로 저장한 sb를 다시 반대로 전환하여 문자열로 변환 후 주어진 문제의 결과로 반환한다.
  - StringBuilder의 insert(int offset, char c) 메서드는 offset까지 포인터를 이동하여 c를 삽입하고 해당 위치 값들을 뒤로 이동시키기 때문에, append(char c) 메서드와 reverse()을 활용하는 것이 시간 복잡도가 더 낮아진다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ConvertANumberToHexadecimal.java){:target="_blank"}에서 확인 가능합니다.