---
title: "Leetcode Java Day of the Week"
excerpt: "Leetcode Easy - 'Day of the Week' 문제 Java 풀이"
last_modified_at: 2024-09-18T10:30:00
header:
  image: /assets/images/leetcode/day-of-the-week.png
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
[Link](https://leetcode.com/problems/day-of-the-week/){:target="_blank"}

# 코드
```java
class Solution {

  private String[] days = new String[] { "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" };

  public String dayOfTheWeek(int day, int month, int year) {
    if (month < 3) {
      month += 12;
      year -= 1;
    }
    int century = year / 100;
    year %= 100;
    return days[((((century / 4) - (2 * century) + year + (year / 4) + ((13 * (month + 1)) / 5) + day - 1) % 7) + 7) % 7];
  }

}
```

# 결과
[Link](https://leetcode.com/problems/day-of-the-week/submissions/1393828670/){:target="_blank"}

# 설명
1. year년 month월 day일자가 무슨 요일인지 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- 전역 변수인 days는 요일에 따라 반환할 결과를 저장한 변수이다.
- month가 3 미만인 경우, month에 12를 더하고 yaer에 1을 감소시킨다.
- century는 세기를 저장할 변수로, year을 100으로 나눈 몫을 저장한다.
- year에 세기를 제외한 100을 나눈 나머지를 넣어준다.

3. [Zeller's congruence](https://en.wikipedia.org/wiki/Zeller%27s_congruence){:target="_blank"} 방식으로 days에서 $\frac{century}{4} - (2 \times century) + year + \frac{year}{4} + \frac{13 \times (month + 1)}{5} + day - 1$의 결과에 7을 나눈 나머지에 7을 더한 후 다시 7을 나눈 나머지 번째 값을 꺼내 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DayOfTheWeek.java){:target="_blank"}에서 확인 가능합니다.