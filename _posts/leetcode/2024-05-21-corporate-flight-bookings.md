---
title: "Leetcode Java Corporate Flight Bookings"
excerpt: "Leetcode Corporate Flight Bookings Java"
last_modified_at: 2024-05-21T19:00:00
header:
  image: /assets/images/leetcode/corporate-flight-bookings.png
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
[Link](https://leetcode.com/problems/corporate-flight-bookings/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] corpFlightBookings(int[][] bookings, int n) {
    int[] result = new int[n];
    for (int[] booking : bookings) {
      result[booking[0] - 1] += booking[2];
      if (booking[1] < n) {
        result[booking[1]] -= booking[2];
      }
    }
    for (int i = 1; i < n; i++) {
      result[i] += result[i - 1];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/corporate-flight-bookings/submissions/1263872939/){:target="_blank"}

# 설명
1. 아래의 규칙을 만족하는 n개의 노선이 저장된 bookings를 이용하여 n개 노선의 각 좌석의 합계를 구하는 문제이다.
- bookings[i] = [first<sub>i</sub>, last<sub>i</sub>, seats<sub>i</sub>]로, i번째 항공편은 first 부터 last까지 노선의 좌석이 seats개임을 의미한다.

2. result는 각 노선 별 좌석의 수를 계산할 변수로, n 크기의 정수 배열로 초기화한다.

3. bookings의 각 배열 값을 순차적으로 booking에 넣어 아래를 수행한다.
- result의 $booking[0] - 1$번째 위치인 시작 노선에 booking[2]인 좌석 수를 더해준다.
- booking[1]이 n 미만인 경우, result의 booking[1]번째 값에 booking[2]인 좌석 수를 감소시켜준다.

4. result의 시작부터 끝까지 다음 위치에 현재 값을 누계하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CorporateFlightBookings.java){:target="_blank"}에서 확인 가능합니다.