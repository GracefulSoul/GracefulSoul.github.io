---
title: "Leetcode Java Binary Gap"
excerpt: "Leetcode Binary Gap Java"
last_modified_at: 2023-03-09T19:20:00
header:
  image: /assets/images/leetcode/binary-gap.png
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
[Link](https://leetcode.com/problems/binary-gap){:target="_blank"}

# 코드
```java
class Solution {

  public int binaryGap(int n) {
    int result = 0;
    for (int i = -32; n > 0; n /= 2, i++) {
      if (n % 2 == 1) {
        result = Math.max(result, i);
        i = 0;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/binary-gap/submissions/912010329/){:target="_blank"}

# 설명
1. 양의 정수 n을 이진 표현식으로 변환하였을 때, 1 사이가 가장 긴 거리를 반환하는 문제이다.
- 예를 들어 "1001"의 경우, 두 1 사이의 거리는 3이다.

2. result는 1 사이가 가장 긴 거리를 저장할 변수로, 0으로 초기화한다.

3. i가 -32부터 n이 0 이상일 때 까지 n에 2로 나눈 몫을 넣어주고 i를 증가시키며 아래를 반복한다.
- n을 2로 나눈 나머지가 1인 경우, result에 result와 i 중 큰 값을 넣어주고 i를 0으로 초기화시킨다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 해설
- i가 -32부터 1씩 증가하는 이유는 int를 이진 표현식으로 변환할 때 32자리로 표현되기 때문이다.
- n이 홀수일 때, result와 i 중 큰 값을 넣는 이유는 아래와 같다.
  - 처음 발생한 위치를 result에 표시하고 i를 초기화 시킨다.
  - i를 증가시키며 다음 1이 발생하는 위치와 거리를 계산한다.
  - 기존 저장된 result의 길이와 현재 계산된 거리 중 큰 값을 result에 저장하고, i를 0으로 초기화 하여 위의 수행을 반복한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinaryGap.java){:target="_blank"}에서 확인 가능합니다.