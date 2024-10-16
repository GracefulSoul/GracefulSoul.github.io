---
title: "Leetcode Java UTF-8 Validation"
excerpt: "Leetcode UTF-8 Validation Java 풀이"
last_modified_at: 2022-02-21T18:00:00
header:
  image: /assets/images/leetcode/utf-8-validation.png
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
[Link](https://leetcode.com/problems/utf-8-validation/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean validUtf8(int[] data) {
    int bytes = 0;
    for (int num : data) {
      int mask = 128;
      if (bytes == 0) {
        while ((mask & num) != 0) {
          bytes++;
          mask >>= 1;
        }
        if (bytes > 4 || bytes == 1) {
          return false;
        }
      } else {
        if ((num & mask) == 0 || (num & (mask >> 1)) != 0) {
          return false;
        }
      }
      if (bytes != 0) {
        bytes -= 1;
      }
    }
    return bytes == 0;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/645870882/){:target="_blank"}

# 설명
1. 주어진 정수 배열 data가 UTF-8 인코딩인지 검증하는 문제이다.
- 올바른 UTF-8는 아래와 같다.
- | Char. number range | UTF-8 octet sequence |
| (hexadecimal) | (binary) |
|:--------|:--------|
| 0000 0000-0000 007F | 0xxxxxxx |
| 0000 0080-0000 07FF | 110xxxxx 10xxxxxx |
| 0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx |
| 0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx |

2. 문자열의 shift 횟수를 저장할 bytes를 0으로 정의한다.

3. data를 반복하여 검증을 수행한다.
- 검증을 수행할 mask를 128로 정의한다.
- bytes가 0인 경우, 아래를 수행한다.
  - mask와 num의 AND(&) 비트 연산의 결과가 0이 아닌 경우, bytes를 증가시키고 mask의 bit를 우측으로 한 칸 이동시킨다.
  - bytes가 4보다 크거나 1인 경우 UTF-8 인코딩이 아니므로, false를 주어진 문제의 결과로 반환한다.
- bytes가 0이 아닌 경우, 아래를 수행한다.
  - num과 mask의 AND(&) 비트 연산의 결과가 0이거나 num과 mask의 bit를 우측으로 한 칸 이동시킨 값의 AND(&) 비트 연산의 결과가 0이 아닌 경우, false를 주어진 문제의 결과로 반환한다.
- bytes가 0이 아닌 경우, bytes를 감소시킨다.

4. 반복이 완료되면 bytes가 0인지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UTF8Validation.java){:target="_blank"}에서 확인 가능합니다.