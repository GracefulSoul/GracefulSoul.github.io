---
title: "Leetcode Java Lemonade Change"
excerpt: "Leetcode Lemonade Change Java"
last_modified_at: 2023-03-03T20:40:00
header:
  image: /assets/images/leetcode/lemonade-change.png
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
[Link](https://leetcode.com/problems/lemonade-change){:target="_blank"}

# 코드
```java
class Solution {

  public boolean lemonadeChange(int[] bills) {
    int[] changes = new int[] { 0, 0 };
    for (int bill : bills) {
      if (bill == 5) {
        changes[0]++;
      } else if (bill == 10) {
        changes[0]--;
        changes[1]++;
      } else if (changes[1] > 0) {
        changes[1]--;
        changes[0]--;
      } else {
        changes[0] -= 3;
      }
      if (changes[0] < 0) {
        return false;
      }
    }
    return true;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/lemonade-change/submissions/908282536/){:target="_blank"}

# 설명
1. 한 잔에 5달러인 레모네이드를 bills 순서대로 판매할 때, 거스름돈이 없이 판매하여 순차적으로 거스름돈을 반환할 수 있는지 검증하는 문제이다.
- 고객은 한 번에 한 잔의 레모네이드를 구매하며 5, 10, 20 달러 지폐를 지불한다.

2. changes는 5달러와 10달러의 거스름돈의 수를 저장할 배열로, 두 값을 0으로 초기화한다.

3. bills를 bill에 넣어 아래를 반복한다.
- bill이 5인 경우, 5달러의 거스름돈이 생겼으므로 5달러의 갯수를 증가시킨다.
- 위가 아니면서 bill이 10인 경우, 5달러의 거스름돈을 제공하고 10 달러의 거스름돈이 생겼으므로 5달러의 갯수를 증가시키고 10달러의 수를 감소시킨다.
- 위가 아니면서 changes의 두 번째 값인 10달러의 거스름돈이 1개 이상인 경우, 20달러 지폐를 받았으므로 5달러와 10달러를 하나씩 감소시킨다.
- 위가 아니면 10달러의 거스름돈이 없으므로, 5달러의 수를 3개 감소시킨다.
- 5달러의 수가 0 미만인 경우 거스름돈 한도를 초과하였으므로, false를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 순차적으로 거스름돈을 반환하였으므로 true를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/LemonadeChange.java){:target="_blank"}에서 확인 가능합니다.