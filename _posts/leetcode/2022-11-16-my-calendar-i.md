---
title: "Leetcode Java My Calendar I"
excerpt: "Leetcode My Calendar I Java"
last_modified_at: 2022-11-16T20:00:00
header:
  image: /assets/images/leetcode/my-calendar-i.png
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
[Link](https://leetcode.com/problems/my-calendar-i){:target="_blank"}

# 코드
```java
class MyCalendar {

  private TreeMap<Integer, Integer> bookings;

  public MyCalendar() {
    this.bookings = new TreeMap<>();
  }

  public boolean book(int start, int end) {
    Map.Entry<Integer, Integer> booking = this.bookings.floorEntry(--end);
    if (booking == null || booking.getValue() < start) {
      this.bookings.put(start, end);
      return true;
    } else {
      return false;
    }
  }

}

/**
 * Your MyCalendar object will be instantiated and called as such:
 * MyCalendar obj = new MyCalendar();
 * boolean param_1 = obj.book(start,end);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/844502070/){:target="_blank"}

# 설명
1. 날자가 겹치지 않게 관리하는 일정 관리 시스템인 MyCalendar 클래스를 완성하는 문제이다.
- 일정은 [start, end) 형태로 주입되며, 반 열림 구간인 start <= x < end 를 만족한다.
- 생성자인 MyCalendar()는 일정 관리 객체를 초기화한다.
- 메서드인 book(int start, int end)은 [start, end) 구간의 일정 추가가 가능하면 일정 관리 시스템에 추가 후 true를 반환하고, 겹치는 일정이 존재하면 일정을 추가하지 않고 end를 반환한다.

2. bookings는 일정을 저장하고 관리할 객체로 구간 관리를 하기 위해 TreeMap으로 정의한다.

3. 생성자인 MyCalendar()를 완성한다.
- 일정 관리를 하기 위한 bookings를 TreeMap으로 초기화한다.

4. 메서드인 book(int start, int end)을 완성한다.
- 일정은 반열림 구간이므로 end를 1 감소시키고 bookings에서 해당 값보다 같거나 작은 값 중 가장 큰 값이 키인 Entry 객체를 booking에 넣어준다.
- booking이 null이거나 booking의 값이 start보다 작은 경우 예약 가능한 일정이므로, bookings에 키가 start에 값은 end로 추가하고 true를 반환한다.
- 위의 경우가 아니라면 예약 불가능하므로 false를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MyCalendarI.java){:target="_blank"}에서 확인 가능합니다.