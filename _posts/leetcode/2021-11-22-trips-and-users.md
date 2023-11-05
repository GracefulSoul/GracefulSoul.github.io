---
title: "Leetcode MySQL Trips and Users"
excerpt: "Leetcode Trips and Users MySQL 풀이"
last_modified_at: 2021-11-22T12:00:00
header:
  image: /assets/images/leetcode/trips-and-users.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - MySQL

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/problems/trips-and-users/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT request_at AS 'Day',
  ROUND(COUNT(IF(status != 'completed', TRUE, NULL)) / COUNT(*), 2) AS 'Cancellation Rate'
FROM Trips
WHERE request_at BETWEEN '2013-10-01' AND '2013-10-03'
AND client_id NOT IN (
  SELECT users_Id FROM Users WHERE banned = 'Yes'
)
AND driver_id NOT IN (
  SELECT users_Id FROM Users WHERE banned = 'Yes'
)
GROUP BY request_at;
```

# 결과
[Link](https://leetcode.com/submissions/detail/590738851/){:target="_blank"}

# 설명
1. 2013년 10월 01일부터 03일까지 날자 별 취소율을 구하는 문제이다.

2. Trips 테이블에 request_at의 날자가 '2013-10-01'부터 '2013-10-03'까지 데이터를 조회한다.

3. 추가적으로 client_id와 dirver_id가 Users Table 내 banned가 'Yes'인 user_id를 제외한다.

4. request_at에 대한 날자 별 데이터를 집계하기 위하여 GROUP BY절을 이용한다.

5. 'Cancellation Rate'를 구하기 위해 status가 completed가 아닌 데이터의 개수와 전체 개수를 나눈 후, 예제와 동일하게 소수점 2자리까지 반올림 하여 표시한다.