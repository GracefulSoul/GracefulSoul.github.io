---
title: "Leetcode Java Swap Adjacent in LR String"
excerpt: "Leetcode Swap Adjacent in LR String Java"
last_modified_at: 2022-12-22T12:55:00
header:
  image: /assets/images/leetcode/swap-adjacent-in-lr-string.png
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
[Link](https://leetcode.com/problems/swap-adjacent-in-lr-string){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canTransform(String start, String end) {
    char[] startCharArray = start.toCharArray();
    char[] endCharArray = end.toCharArray();
    int length = startCharArray.length;
    int next = 1;
    for (int idx = 0; idx < length; idx++) {
      if (startCharArray[idx] == endCharArray[idx]) {
        continue;
      }
      if ((startCharArray[idx] == 'R' && endCharArray[idx] == 'X')
          || (endCharArray[idx] == 'L' && startCharArray[idx] == 'X')) {
        next = Math.max(next, idx + 1);
        while (next < length && startCharArray[next] == startCharArray[idx]) {
          next++;
        }
        if (next == length || startCharArray[next] != endCharArray[idx]) {
          return false;
        }
        startCharArray[next] = startCharArray[idx];
      } else {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/swap-adjacent-in-lr-string/submissions/863541987/){:target="_blank"}

# 설명
1. 'L', 'R', 'X' 로 이루어진 start를 아래의 규칙대로 변환되는 문자열이 end에 존재하는지 검증하는 문제이다.
- "XL"를 "LX"로 변환.
- "RX"를 "XR"로 변환.

2. 문제 풀이에 필요한 변수를 정의한다.
- startCharArray는 start를 문자 배열로 변환하여 저장한 변수이다.
- endCharArray는 end를 문자 배열로 변환하여 저장한 변수이다.
- length는 startCharArray의 길이를 저장한 변수이다.
- next는 다음 위치를 지정할 위치 변수로, 처음 시작하는 0보다 큰 1로 초기화한다.

3. 0부터 length까지 idx를 증가시키며 아래를 반복한다.
- startCharArray의 idx번째 문자와 endCharArray의 idx번째 문자가 동일한 경우, 다음 위치로 반복을 계속 수행한다.
- startCharArray의 idx번째 문자가 'R'이면서 endCharArray의 idx번째 문자가 'X'이거나 endCharArray의 idx번째 문자가 'L'이면서 startCharArray의 idx번째 문자가 'X'인 경우 아래를 수행한다.
  - next에 next와 $idx + 1$ 중 큰 값을 넣어준다.
  - next가 length 미만이면서 startCharArray의 next번째 문자가 startCharArray의 idx번째 문자와 동일할 때 까지 next를 계속 증가시킨다.
  - next가 length와 동일한 마지막 위치거나 startCharArray의 next번째 문자가 startCharArray의 idx번째 문자가 달라 변환이 가능한 경우, false를 주어진 문제의 결과로 반환한다.
  - startCharArray의 next번째 문자에 idx번째 문자를 넣어 확인한 문자를 제거한다.
- 위의 경우가 아니라면 변환 가능한 문자가 이어지므로, false를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 모든 변환 가능한 문자가 없으므로, true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SwapAdjacentInLRString.java){:target="_blank"}에서 확인 가능합니다.