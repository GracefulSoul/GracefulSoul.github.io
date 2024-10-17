---
title: "Leetcode Java Extra Characters in a String"
excerpt: "Leetcode Medium - 'Extra Characters in a String' 문제 Java 풀이"
last_modified_at: 2023-09-02T17:40:00
header:
  image: /assets/images/leetcode/extra-characters-in-a-string.png
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
[Link](https://leetcode.com/problems/extra-characters-in-a-string){:target="_blank"}

# 코드
```java
class Solution {

  public int minExtraChar(String s, String[] dictionary) {
    int length = s.length();
    int[] dp = new int[length + 1];
    for (int i = length - 1; i >= 0; i--) {
      String str = s.substring(i);
      dp[i] = dp[i + 1] + 1;
      for (int j = 0; j < dictionary.length; j++) {
        if (str.startsWith(dictionary[j])) {
          dp[i] = Math.min(dp[i], dp[i + dictionary[j].length()]);
        }
      }
    }
    return dp[0];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/extra-characters-in-a-string/submissions/1038290323/){:target="_blank"}

# 설명
1. 문자열 s에서 dictionary에 존재하는 문자열을 겹치지 않도록 최적의 방법으로 제거하고 남은 문자열의 수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 문자열 s의 길이를 저장한 변수이다.
- dp는 최적의 방법으로 제거하고 남은 문자열의 수를 계산하기 위한 변수로, $length + 1$ 크기의 정수 배열로 초기화한다.

3. $length - 1$ 부터 0 이상까지 i를 감소시키며 아래를 반복한다.
- str에 s의 i번째 자리 이후의 문자열을 잘라 넣어준다.
- dp[i]에 이전 횟수인 dp[$i + 1$]에 1을 더해서 넣어준다.
- 0부터 dictionary의 길이 미만까지 dictionary의 문자열 중 str의 시작 부분과 일치하는 문자열이 있는 경우, dp[i]에 현재 값과 dp의 일치하는 문자열의 길이에 i를 더한 위치의 값 중 작은 값을 넣어준다.

4. 반복이 완료되면 남은 문자열의 수가 저장된 dp[0]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ExtraCharactersInAString.java){:target="_blank"}에서 확인 가능합니다.