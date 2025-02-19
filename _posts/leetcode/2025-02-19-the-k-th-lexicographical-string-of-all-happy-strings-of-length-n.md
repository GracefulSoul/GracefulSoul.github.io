---
title: "Leetcode Java The k-th Lexicographical String of All Happy Strings of Length n"
excerpt: "Leetcode - 'The k-th Lexicographical String of All Happy Strings of Length n' 문제 Java 풀이"
last_modified_at: 2025-02-19T13:40:00
header:
  image: /assets/images/leetcode/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n.png
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
[Link](https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/){:target="_blank"}

# 코드
```java
class Solution {

  public String getHappyString(int n, int k) {
    int shift = 1 << (n - 1);
    if (k > 3 * shift) {
      return "";
    } else {
      int c = 'a' + ((k - 1) / shift);
      StringBuilder sb = new StringBuilder(Character.toString(c));
      while (shift > 1) {
        k = ((k - 1) % shift) + 1;
        shift >>= 1;
        if ((k - 1) / shift == 0) {
          c = c == 'a' ? 'b' : 'a';
        } else {
          c = c == 'c' ? 'b' : 'c';
        }
        sb.append((char) c);
      }
      return sb.toString();
    }
  }

}
```

# 결과
[Link](https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/submissions/1548094566/){:target="_blank"}

# 설명
1. 아래 규칙을 만족하는 n 길이의 사전적인 순서가 k 번째 문자열을 생성하는 문제이다.
- 문자열은 'a', 'b', 'c'로 구성된다.
- 붙어있는 두 문자는 동일할 수 없다.

2. shift는 1의 비트를 $n - 1$번 좌측으로 이동시킨 값을 저장한 변수다.

3. k가 $3 \times shift$ 값을 초과하는 조건을 만족하는 문자열 생성이 불가능한 경우, 빈 문자열을 주어진 문제의 결과로 반환한다.

4. k가 $3 \times shift$ 값 이하인 조건을 만족하는 문자열 생성이 가능한 경우, 아래를 수행한다.
- 문자열 생성에 필요한 변수를 정의한다.
  - c는 $'a' + \frac{k - 1}{shift}$인 처음 시작할 수 있는 작은 문자의 아스키 코드 10진수 값을 넣어준다.
  - sb는 결과 문자열 생성에 필요한 변수로, 동적 문자열 생성을 위한 StringBuilder로 초기화하고 c를 첫 문자로 넣어준다.
- shift가 1 초과일 때까지 아래를 반복한다.
  - k에 $\frac{k - 1}{shift}$의 나머지 값에 1을 더한 값을 넣어 다음 문자열의 순서를 저장한다.
  - shift의 비트를 우측으로 한 칸 이동시켜 수행 횟수를 차감한다.
  - $\frac{k - 1}{shift}$의 값이 0인 경우, c에 c가 'a'면 'b'의 값을 그 외는 'a'의 값을 넣어 다음 문자를 저장한다.
  - $\frac{k - 1}{shift}$의 값이 0이 아닌 경우, c에 c가 'c'면 'b'의 값을 그 외는 'c'의 값을 넣어 다음 문자를 저장한다.
  - sb에 c를 문자로 변환하여 넣어주고 다시 반복한다.

5. 반복이 완료되면 완성된 sb를 문자열로 반환하여 주어진 문제의 결과로 반환한다.

# 해설
- 길이가 n인 문자열은 $3 \times 2^(n - 1)$개의 문자열을 만들 수 있으므로, 생성 가능한지 여부는 상한 값을 1의 비트를 $n - 1$번 좌측으로 이동시킨 값으로 설정 가능하다.
- shift를 감소시키면서 $\frac{k - 1}{shift}$의 값이 0인지 검증하는 이유는, 다음 문자의 순서에 따라 문자가 결정 가능하여 동일한 문자를 반복하여 넣지 않게 할 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TheKthLexicographicalStringOfAllHappyStringsOfLengthN.java){:target="_blank"}에서 확인 가능합니다.