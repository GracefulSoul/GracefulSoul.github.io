---
title: "Leetcode Java Day of the Year"
excerpt: "Leetcode Easy - 'Day of the Year' 문제 Java 풀이"
last_modified_at: 2024-08-10T18:30:00
header:
  image: /assets/images/leetcode/day-of-the-year.png
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
[Link](https://leetcode.com/problems/day-of-the-year/){:target="_blank"}

# 코드
```java
class Solution {

  private static int[] DAYS = new int[] { 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 };

  public int dayOfYear(String date) {
    int months = Integer.parseInt(date.substring(5, 7));
    int result = months > 2 && this.isLeapYears(Integer.parseInt(date.substring(0, 4))) ? 1 : 0;
    for (int i = 0; i < months - 1; i++) {
      result += DAYS[i];
    }
    return result + Integer.parseInt(date.substring(8));
  }

  private boolean isLeapYears(int year) {
    return year % 4 == 0 && (year % 400 == 0 || year % 100 != 0);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/day-of-the-year/submissions/1350804105/){:target="_blank"}

# 설명
1. "YYYY-MM-DD" 날자 포멧으로 date가 주어지면 해당 연도의 몇 번째 일자인지 구하는 문제이다.

2. DAYS는 월별 기준 일수를 저장한 변수로 윤달인 경우를 제외하고 값을 넣어 저장한 변수이다.

3. 문제 풀이에 필요한 변수를 정의한다.
- months는 date의 월을 정수로 변환한 변수이다.
- result는 해당 연도의 일자를 저장할 변수로, 아래의 각 경우에 따라 값을 초기화한다.
  - months가 2보다 큰 윤달 일자가 포함되면서 date의 연도가 윤달에 해당하면 1로 초기화한다.
  - 위의 경우가 아니라면 0으로 초기화한다.

4. 0부터 $months - 1$까지 i를 증가시키면서 result에 DAYS[i]의 값을 누계한다.

5. 반복이 완료되면 result에 현재 일자를 더해서 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DayOfTheYear.java){:target="_blank"}에서 확인 가능합니다.