---
title: "Leetcode Java Minimum Bit Flips to Convert Number"
excerpt: "Leetcode Minimum Bit Flips to Convert Number Java"
last_modified_at: 2024-09-11T18:00:00
header:
  image: /assets/images/leetcode/minimum-bit-flips-to-convert-number.png
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
[Link](https://leetcode.com/problems/minimum-bit-flips-to-convert-number/){:target="_blank"}

# 코드
```java
class Solution {

  public int minBitFlips(int start, int goal) {
    int result = 0;
    int bit = start ^ goal;
    while (bit != 0) {
      result += bit & 1;
      bit >>= 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-bit-flips-to-convert-number/submissions/1386491795/){:target="_blank"}

# 설명
1. start에서 goal가 되기까지 비트 변환의 최소 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 비트 변환의 최소 횟수를 저장할 변수로, 0으로 초기화한다.
- bit는 start와 goal의 XOR(^) 비트 연산의 결과를 저장한 변수이다.

3. bit가 0이 아닐 때 까지 result에 bit와 1의 AND(&) 비트 연산인 변경 횟수를 더한 후 bit를 우측으로 한 칸 이동한다.

4. 위를 통해 계산된 횟수인 result를 주어진 문제의 결과로 반환한다.

# 해설
- start와 goal의 XOR(^) 비트 연산의 결과는 두 숫자의 비트 값이 일치하지 않는 비트만 추려낸 동일하게 변경하기 위한 갯수이다.
- bit와 1을 AND(&) 비트 연산을 통해 result에 값을 더한 후 bit를 우측으로 한 칸 이동하는 이유는, 위를 통해 변경해야 할 1 비트의 갯수를 계산하기 위함이다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumBitFlipsToConvertNumber.java){:target="_blank"}에서 확인 가능합니다.