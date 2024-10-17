---
title: "Leetcode MySQL Exchange Seats"
excerpt: "Leetcode - 'Exchange Seats MySQL 풀이"
last_modified_at: 2022-08-17T19:10:00
header:
  image: /assets/images/leetcode/exchange-seats.png
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
[Link](https://leetcode.com/problems/exchange-seats/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT
    CASE WHEN id % 2 = 0 THEN id - 1
         WHEN id % 2 = 1 AND id < (SELECT COUNT(*) FROM Seat) THEN id + 1
         ELSE id
    END AS id, student
FROM Seat
ORDER BY id
```

# 결과
[Link](https://leetcode.com/submissions/detail/775944674/){:target="_blank"}

# 설명
1. Seat 테이블 내 연속된 순서의 학생들의 id를 바꾸는 문제이다.
- 단, 학생의 수가 홀수인 경우 마지막 학생의 id는 바꾸지 않는다.