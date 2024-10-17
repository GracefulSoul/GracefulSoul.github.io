---
title: "Leetcode Java 2 Keys Keyboard"
excerpt: "Leetcode - '2 Keys Keyboard' 문제 Java 풀이"
last_modified_at: 2022-09-07T19:30:00
header:
  image: /assets/images/leetcode/2-keys-keyboard.png
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
[Link](https://leetcode.com/problems/2-keys-keyboard){:target="_blank"}

# 코드
```java
class Solution {

  public int minSteps(int n) {
    int result = 0;
    for (int idx = 2; idx * idx <= n;) {
      if (n % idx == 0) {
        result += idx;
        n /= idx;
      } else {
        idx++;
      }
    }
    if (n != 1) {
      result += n;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/793774891/){:target="_blank"}

# 설명
1. A 한 문자만 존재하는 메모장에서 모두 복사, 붙여넣기 두 기능만 사용 가능했을 때 A 문자를 정확히 n번 나타낼 수 있는 최소 기능 사용 횟수를 구하는 문제이다.

2. 최소 횟수를 담기 위한 result를 0으로 초기화한다.

3. n이 2이면 복사 -> 붙여넣기 순으로 되므로 최소 횟수인 2부터 $idx^2$이 n 이하일 때까지 아래를 반복한다.
- n을 idx로 나눈 나머지가 0이면 계산된 순번을 반복할 수 있으므로, result에 idx를 더해주고 n에 n을 idx로 나눈 값을 넣어준다.
- 위의 경우가 아니라면 idx를 증가시켜 붙여넣기를 추가로 수행했을 경우로 계산을 수행한다.

4. n이 1이 아닌 경우 추가로 기능을 수행해야 하므로, result에 남은 n을 더해준다.

5. 최소 기능 사용 횟수를 계산한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/TwoKeysKeyboard.java){:target="_blank"}에서 확인 가능합니다.