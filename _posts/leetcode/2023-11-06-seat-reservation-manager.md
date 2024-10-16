---
title: "Leetcode Java Seat Reservation Manager"
excerpt: "Leetcode Seat Reservation Manager Java"
last_modified_at: 2023-11-06T19:20:00
header:
  image: /assets/images/leetcode/seat-reservation-manager.png
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
[Link](https://leetcode.com/problems/seat-reservation-manager){:target="_blank"}

# 코드
```java
class SeatManager {

  private boolean[] seats;
  private int reserved;
  private int unreserved;

  public SeatManager(int n) {
    this.seats = new boolean[n + 1];
    this.reserved = 1;
    this.unreserved = 0;
  }

  public int reserve() {
    if (unreserved == 0) {
      this.seats[reserved] = true;
      return this.reserved++;
    } else {
      for (int i = 1; i < this.seats.length; i++) {
        if (!this.seats[i]) {
          this.seats[i] = true;
          this.unreserved--;
          return i;
        }
      }
    }
    return -1;
  }

  public void unreserve(int seatNumber) {
    this.unreserved++;
    this.seats[seatNumber] = false;
  }

}

/**
 * Your SeatManager object will be instantiated and called as such:
 * SeatManager obj = new SeatManager(n);
 * int param_1 = obj.reserve();
 * obj.unreserve(seatNumber);
 */
```

# 결과
[Link](https://leetcode.com/problems/seat-reservation-manager/submissions/1092716384/){:target="_blank"}

# 설명
1. [1, n] 범위의 자석의 예약 관리하는 SeatManager 클래스를 완성하는 문제이다.
- 생성자인 SeatManager(int n)는 [1, n] 범위의 자리를 초기화한다.
- 메서드인 reserve()는 가장 작은 숫자의 예약하지 않은 좌석을 가져와 예약하고 번호를 반환한다.
- 메서드인 unreserve(int seatNumber)는 seatNumber의 좌석을 예약 해지한다.

2. 좌석 예약을 위한 전역 변수를 정의한다.
- seats는 좌석을 관리하기 위한 변수이다.
- reserved는 예약된 좌석을 계산하기 위한 변수이다.
- unreserved는 예약을 해지한 좌석을 계산하기 위한 변수이다.

3. 생성자인 SeatManager(int n)를 완성한다.
- seats를 $n + 1$ 크기의 부울 배열로 초기화한다.
- reserved는 첫 예약의 시작 위치인 1로 초기화한다.
- unreserved는 해지한 예약이 없으므로 0으로 초기화한다.

4. 메서드인 reserve()를 완성한다.
- unreserved가 0인 경우, seats[reserved]의 값을 true로 바꾸어주고 reserved를 증가시켜준다.
- 위의 경우가 아니라면 seats의 빈 좌석을 찾아 true로 바꾸고, unreserved를 증가시킨 후 해당 위치를 반환한다.

5. 메서드인 unreserve(int seatNumber)를 완성한다.
- unreserved를 증가시키고 seats[seatNumber]의 값을 false인 빈 자리로 바꾸어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SeatReservationManager.java){:target="_blank"}에서 확인 가능합니다.