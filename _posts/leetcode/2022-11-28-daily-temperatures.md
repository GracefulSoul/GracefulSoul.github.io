---
title: "Leetcode Java Daily Temperatures"
excerpt: "Leetcode Daily Temperatures Java"
last_modified_at: 2022-11-28T14:30:00
header:
  image: /assets/images/leetcode/daily-temperatures.png
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
[Link](https://leetcode.com/problems/daily-temperatures){:target="_blank"}

# 코드
```java
class Solution {

  public int[] dailyTemperatures(int[] temperatures) {
    int length = temperatures.length;
    int lastTemperature = 0;
    int[] result = new int[length];
    for (int idx = length - 1; idx >= 0; idx--) {
      int currentTemperature = temperatures[idx];
      if (currentTemperature >= lastTemperature) {
        lastTemperature = currentTemperature;
        continue;
      }
      int days = 1;
      while (temperatures[idx + days] <= currentTemperature) {
        days += result[idx + days];
      }
      result[idx] = days;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/849858202/){:target="_blank"}

# 설명
1. 일자별 온도 정보를 저장하는 temperatures를 이용하여 현재 온도에서 더 따뜻한 온도가 되는 날까지의 일수 차이를 계산하여 반환하는 문제이다.
- 더 따뜻한 온도의 날자 정보가 없는 경우, 0을 넣어준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 temperatures의 길이를 저장한 변수이다.
- lastTemperature는 이전 온도 정보를 저장할 변수로, 0으로 초기화한다.
- result는 일수 차이를 계산해서 넣어줄 배열로, temperatures와 동일한 크기인 length 크기의 정수 배열로 초기화한다.

3. $length - 1$부터 0까지 idx를 감소시키면서 아래를 수행한다.
- temperatures의 idx번째 온도 정보를 currentTemperature에 임시 저장한다.
- currentTemperature가 lastTemperature보다 크거나 같은 경우, lastTemperature에 currentTemperature를 저장하고 다음 반복을 수행한다.
- 날자 차이를 계산할 days를 1로 초기화하고, temperatures의 현재 위치 이후인 $idx + days$번째 온도 정보부터 currentTemperature 이하인 경우, days에 result의 $idx + days$ 번째 위치 값을 더해준다.
- 위의 반복이 완료되면 result의 idx번째 위치에 계산된 days를 넣어준다.

4. 반복이 완료되면 날자 차이 값을 계산한 result를 주어진 문제의 결과로 반환한다.


# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DailyTemperatures.java){:target="_blank"}에서 확인 가능합니다.