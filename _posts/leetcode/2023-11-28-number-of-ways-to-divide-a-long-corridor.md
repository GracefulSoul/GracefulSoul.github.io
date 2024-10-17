---
title: "Leetcode Java Number of Ways to Divide a Long Corridor"
excerpt: "Leetcode Hard - 'Number of Ways to Divide a Long Corridor' 문제 Java 풀이"
last_modified_at: 2023-11-28T20:40:00
header:
  image: /assets/images/leetcode/number-of-ways-to-divide-a-long-corridor.png
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
[Link](https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfWays(String corridor) {
    char[] charArray = corridor.toCharArray();
    int length = charArray.length;
    int seat = 0;
    long result = 1;
    for (int i = 0; i < length; i++) {
      if (charArray[i] == 'S') {
        seat++;
        while (++i < length && charArray[i] != 'S') {
        }
        if (i < length && charArray[i] == 'S') {
          seat++;
        }
        int divider = 1;
        while (++i < length && charArray[i] != 'S') {
          divider++;
        }
        if (divider > 1 && i < length) {
          result = (result * divider) % 1000000007;
        }
        i--;
      }
    }
    return seat != 0 && seat % 2 == 0 ? (int) result : 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-ways-to-divide-a-long-corridor/submissions/1108107032/){:target="_blank"}

# 설명
1. corridor를 이용하여 아래의 규칙을 만족하는 복도를 만들 수 있는 경우의 수를 구하는 문제이다.
- corridor 내 'S'는 자리를, 'P'는 식물을 의미한다.
- corridor 시작 전과 끝에는 룸 디바이더로 구성되어 있으며, 복도를 나누기 위해서는 양 쪽 모두 정확히 2개의 좌석이 포함되어야하고 식물의 갯수는 상관 없다.
- 답이 매울 클 수 있으므로 모듈러 $10^9 + 7$을 적용한 값을 반환한다.
- 답이 존재하지 않는 경우, 0을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- charArray는 corridor를 문자 배열로 변환한 변수이다.
- length는 charArray의 길이를 저장한 변수이다.
- seat는 좌석의 갯수를 저장할 변수로, 0으로 초기화한다.
- result는 경우의 수를 저장할 변수로, 값이 매우 클 수 있으므로 long 타입의 1로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며 아래를 수행한다.
- charArray[i]의 문자가 'S'인 좌석의 경우만 아래를 수행하며, 'P'인 식물의 경우 갯수 제한이 없으므로 다음 반복을 수행한다.
- seat를 증가시켜 좌석의 수를 증가시켜주고, i가 legnth 미만이면서 'S'가 아닌 문자일 때 까지 i를 증가시켜준다.
- i를 증가시킨 값이 length 미만이면서 charArray[i]의 문자가 'S'인 경우, seat를 증가시켜 2개로 만들어준다.
- divider는 복도를 만들 수 있는 경우의 수로, 1로 초기화 후 i를 증가시킨 값이 length 미만이면서 charArray[i]의 문자가 'S'가 아닐 때 까지 divider를 증가시켜 경우의 수를 증가시켜준다.
- divider가 1보다 크면서 i가 length 미만인 경우, result에 기존 경우의 수인 result와 현재 위치에서 복도를 만들 수 있는 경우의 수인 divider의 곱에 모듈러 $10^9 + 7$을 적용한 값을 넣어준다.
- 마지막으로 복도 시작 전 위치에서 다시 반복을 수행하기 위하여 i를 감소시켜준다.

4. 반복이 완료되면 아래의 경우를 모두 만족하지 않으면 result를 int로 변환하여, 아니면 0을 주어진 문제의 결과로 반환한다.
- seat가 0인 복도 생성이 불가능한 경우.
- seat의 갯수가 홀수라서 정확히 2개 단위로 복도 생성을 모두 수행하지 못하는 경우.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfWaysToDivideALongCorridor.java){:target="_blank"}에서 확인 가능합니다.