---
title: "Leetcode PostgreSQL Reformat Department Table"
excerpt: "Leetcode Easy - 'Reformat Department Table' 문제 PostgreSQL 풀이"
last_modified_at: 2024-09-08T10:50:00
header:
  image: /assets/images/leetcode/reformat-department-table.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - PostgreSQL

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/problems/reformat-department-table/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT
  id,
  SUM(CASE WHEN month = 'Jan' THEN revenue END) AS Jan_Revenue,
  SUM(CASE WHEN month = 'Feb' THEN revenue END) AS Feb_Revenue,
  SUM(CASE WHEN month = 'Mar' THEN revenue END) AS Mar_Revenue,
  SUM(CASE WHEN month = 'Apr' THEN revenue END) AS Apr_Revenue,
  SUM(CASE WHEN month = 'May' THEN revenue END) AS May_Revenue,
  SUM(CASE WHEN month = 'Jun' THEN revenue END) AS Jun_Revenue,
  SUM(CASE WHEN month = 'Jul' THEN revenue END) AS Jul_Revenue,
  SUM(CASE WHEN month = 'Aug' THEN revenue END) AS Aug_Revenue,
  SUM(CASE WHEN month = 'Sep' THEN revenue END) AS Sep_Revenue,
  SUM(CASE WHEN month = 'Oct' THEN revenue END) AS Oct_Revenue,
  SUM(CASE WHEN month = 'Nov' THEN revenue END) AS Nov_Revenue,
  SUM(CASE WHEN month = 'Dec' THEN revenue END) AS Dec_Revenue
FROM Department
GROUP BY id
```

# 결과
[Link](https://leetcode.com/problems/reformat-department-table/submissions/1382623248/){:target="_blank"}

# 설명
1. Department 테이블에서 월 별 수익을 계산하는 문제이다.
- month 필드의 값은 ["Jan","Feb","Mar","Apr","May","Jun","Jul","Aug","Sep","Oct","Nov","Dec"]가 존재한다.

2. 각 월별 revenue를 id 기준으로 그룹지어 합계를 계산한다.
- 단, 데이터가 없는 경우에 대한 기본 값은 0이 아니라 null이므로 "ELSE 0"으로 기본 값을 치환하지 않아도 된다.