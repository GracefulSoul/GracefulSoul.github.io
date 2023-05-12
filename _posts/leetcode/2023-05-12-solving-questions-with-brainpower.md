---
title: "Leetcode Java Solving Questions With Brainpower"
excerpt: "Leetcode Solving Questions With Brainpower Java"
last_modified_at: 2023-05-12T19:35:00
header:
  image: /assets/images/leetcode/solving-questions-with-brainpower.png
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
[Link](https://leetcode.com/problems/solving-questions-with-brainpower){:target="_blank"}

# 코드
```java
class Solution {

  public long mostPoints(int[][] questions) {
    int length = questions.length;
    long[] dp = new long[length + 1];
    for (int i = length - 1; i >= 0; i--) {
      dp[i] = Math.max(questions[i][0] + dp[Math.min(questions[i][1] + i + 1, length)], dp[i + 1]);
    }
    return dp[0];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/solving-questions-with-brainpower/submissions/948951250/){:target="_blank"}

# 설명
1. 아래의 구성으로 이루어진 questions를 이용하여 최대 얻을 수 있는 시험 점수를 구하는 문제이다.
- questions[i] = [point<sub>i</sub>, brainpower<sub>i</sub>]로, i번째 문제를 맞출 경우 얻을 수 있는 점수와 다음의 문제를 풀 수 없는 수를 의미한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 questions의 길이를 저장한 변수이다.
- dp는 최대 점수를 계산하기 위한 변수로, $length + 1$ 크기의 long 배열로 초기화한다.

3. $length - 1$부터 0 이상까지 i를 감소시키며 아래를 수행한다.
- dp의 i번째 값에 아래의 두 값 중 큰 값인 최대 시험 점수를 넣어준다.
  - dp에서 무시해야 하는 문제의 수인 questions[i][1]의 값에 현재 위치의 다음 값인 $i + 1$을 더한 값과 length 중 작은 값에 해당하는 위치의 값과 questions[i][0]인 점수를 더한 값.
  - dp의 이전까지 최대 값인 $i + 1$번째 값.

4. 반복이 완료되면 최대 점수가 계산된 dp[0]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SolvingQuestionsWithBrainpower.java){:target="_blank"}에서 확인 가능합니다.