---
title: "Leetcode Java Number of Laser Beams in a Bank"
excerpt: "Leetcode Number of Laser Beams in a Bank Java"
last_modified_at: 2024-01-03T11:10:00
header:
  image: /assets/images/leetcode/number-of-laser-beams-in-a-bank.png
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
[Link](https://leetcode.com/problems/number-of-laser-beams-in-a-bank){:target="_blank"}

# 코드
```java
class Solution {

  public int numberOfBeams(String[] bank) {
    int result = 0;
    int prev = 0;
    int curr = 0;
    for (String s : bank) {
      curr = 0;
      for (char c : s.toCharArray()) {
        if (c == '1') {
          curr++;
        }
      }
      if (curr > 0) {
        result += prev * curr;
        prev = curr;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-laser-beams-in-a-bank/submissions/1135169507/){:target="_blank"}

# 설명
1. bank 내 레이저의 갯수를 반환하는 문제이다.
- bank[i]는 '0'과 '1'로 구성된 i번째 행으로, '0'은 빈 셀을 '1'은 보안 장치를 의미한다.
- 아래의 조건을 모두 만족하는 경우, 두 보안 장치 사이에 레이저가 하나 존재한다.
  - r<sub>1</sub>, r<sub>2</sub> 두 장치는 r<sub>1</sub> < r<sub>2</sub>의 다른 두 행에 위치한다.
  - r<sub>1</sub> < i < r<sub>2</sub>인 각 행에 대해 i번째 행에는 보안 장치가 없다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 레이저의 갯수를 저장할 변수로, 0으로 초기화한다.
- prev와 curr은 이전과 현재 행의 보안 장치 갯수를 저장할 변수로, 둘 다 0으로 초기화한다.

3. bank의 문자열을 s에 순차적으로 넣고 아래를 반복한다.
- curr을 0으로 초기화하고 s내 1의 갯수를 넣어준다.
- curr이 0보다 큰 경우, result에 prev의 행과 curr의 행 사이에 존재할 수 있는 레이저 갯수인 $prev \times curr$를 더해주고 prev에 curr을 넣어준다.

4. 반복이 완료되면 레이저의 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfLaserBeamsInABank.java){:target="_blank"}에서 확인 가능합니다.