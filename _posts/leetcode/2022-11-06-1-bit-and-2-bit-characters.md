---
title: "Leetcode Java 1-bit and 2-bit Characters"
excerpt: "Leetcode 1-bit and 2-bit Characters Java"
last_modified_at: 2022-11-06T08:50:00
header:
  image: /assets/images/leetcode/1-bit-and-2-bit-character.png
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
[Link](https://leetcode.com/problems/1-bit-and-2-bit-character){:target="_blank"}

# 코드
```java
class Solution {

  public boolean isOneBitCharacter(int[] bits) {
    int bit = 0;
    for (int idx = bits.length - 2; idx >= 0 && bits[idx] != 0; idx--) {
      bit++;
    }
    return bit % 2 == 0;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/837664588/){:target="_blank"}

# 설명
1. 0으로 끝나는 bits 배열의 값들은 0, 1, 10, 11로 값이 들어가 있으며, 이 값들을 이용하여 마지막 문자가 1비트 문자인지 검증하는 문제이다.

2. bit는 문자의 비트를 계산하기 위한 변수로, 0으로 초기화한다.

3. 마지막 값은 0이므로 무시하고 bits의 길이보다 2 작은 길이부터 idx가 0 이상이고 bits의 idx번째 값이 0이 아닐 때 까지 bit를 증가시킨다.

4. 1비트 문자가 되기 위해선 110, 11110과 같이 bit의 1의 개수가 짝수가 되어야 하므로 bit가 짝수인지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/OneBitAndTwoBitCharacters.java){:target="_blank"}에서 확인 가능합니다.