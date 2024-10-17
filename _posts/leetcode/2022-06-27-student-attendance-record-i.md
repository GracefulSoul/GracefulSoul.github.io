---
title: "Leetcode Java Student Attendance Record I"
excerpt: "Leetcode - 'Student Attendance Record I' 문제 Java 풀이"
last_modified_at: 2022-06-27T19:00:00
header:
  image: /assets/images/leetcode/student-attendance-record-i.png
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
[Link](https://leetcode.com/problems/student-attendance-record-i/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkRecord(String s) {
    return s.indexOf("A") == s.lastIndexOf("A") && !s.contains("LLL");
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/732456688/){:target="_blank"}

# 설명
1. 아래의 각 문자 별 출석 상태를 기준으로 개근상을 받을 수 있는지 여부를 검증하는 문제이다.
- 'A'는 결석을 의미한다.
- 'L'은 지각을 의미한다.
- 'P'는 출석을 의미한다.
- 위 세 값을 이용하여 1번 이하의 결석과 3번 연속 지각하지 않으면 개근상을 받을 수 있다.

2. s 내 결석인 "A"의 첫 위치와 마지막 위치가 동일하고, 3연속 지각인 "LLL"이 없으면 true를 아니면 false를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/StudentAttendanceRecordI.java){:target="_blank"}에서 확인 가능합니다.