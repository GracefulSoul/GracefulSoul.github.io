---
title: "Leetcode Java Broken Calculator"
excerpt: "Leetcode Broken Calculator Java"
last_modified_at: 2023-09-08T18:20:00
header:
  image: /assets/images/leetcode/broken-calculator.png
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
[Link](https://leetcode.com/problems/broken-calculator){:target="_blank"}

# 코드
```java
class Solution {

  public int brokenCalc(int startValue, int target) {
    int result = 0;
    while (target > startValue) {
      if (target % 2 > 0) {
        target++;
      } else {
        target /= 2;
      }
      result++;
    }
    return result + startValue - target;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/broken-calculator/submissions/1043769239/){:target="_blank"}

# 설명
1. 처음 값이 startValue인 계산기를 이용하여 target이 될 때까지 아래의 연산을 이용하여 수행할 경우 최소 작업 횟수를 구하는 문제이다.
- 보이는 숫자에 2를 곱해준다.
- 보이는 숫자에 1을 뺴준다.

2. result는 최소 작업 횟수를 저장할 변수로, 0으로 초기화한다.

3. target이 startValue가 될 때까지 아래를 반복한다.
- target이 홀수인 경우, target을 증가시켜준다.
- target이 짝수인 경우, target에 target을 2로 나눈 값을 넣어준다.
- 위를 수행하였으므로 result를 증가시켜 횟수를 증가시킨다.

4. 반복이 완료되면 result에 $startValue - target$인 오차 값을 더해 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BrokenCalculator.java){:target="_blank"}에서 확인 가능합니다.