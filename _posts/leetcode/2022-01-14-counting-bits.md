---
title: "Leetcode Java Counting Bits"
excerpt: "Leetcode Counting Bits Java 풀이"
last_modified_at: 2022-01-14T19:00:00
header:
  image: /assets/images/leetcode/counting-bits.png
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
[Link](https://leetcode.com/problems/counting-bits/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] countBits(int n) {
    int[] result = new int[n + 1];
    for (int idx = 1; idx <= n; idx++) {
      result[idx] = result[idx & (idx - 1)] + 1;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/619609975/){:target="_blank"}

# 설명
1. 주어진 정수 n을 이용하여 0 ~ n까지 bit 형식에 포함된 1의 갯수를 배열의 각 위치에 넣어 반환하는 문제이다.

2. 결과를 넣을 result 배열을 0 ~ n까지 넣어야 하므로, $n + 1$ 크기로 정의한다.

3. 1부터 n까지 idx를 증가시켜 각 숫자의 bit 형식에 포함된 1의 갯수를 센다.
- result의 idx번째 값에 result의 idx와 $idx - 1$의 AND(&) 비트 연산을 수행한 결과의 위치 값에 1을 더하여 넣어주고, 반복을 계속 수행한다.
  - idx & $idx - 1$의 비트 연산의 수행은 가장 낮은 세트 비트를 삭제한다.
  - 예를 들어 idx가 14인 경우 비트는 1110로, $idx - 1$은 1101로 AND(&) 비트 연산의 결과는 1100이 되므로 1이 2개여서 추가로 1을 더하면 result[14]는 3이 된다.
  - 위의 내용을 정리하면 $result[idx] = result[idx & (idx - 1)] + 1$이 성립한다.

4. 0 ~ n까지 bit 형식에 포함된 1의 갯수를 넣은 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountingBits.java){:target="_blank"}에서 확인 가능합니다.