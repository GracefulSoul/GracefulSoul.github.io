---
title: "Leetcode PostgreSQL Managers with at Least 5 Direct Reports"
excerpt: "Leetcode Medium - 'Managers with at Least 5 Direct Reports' 문제 PostgreSQL 풀이"
last_modified_at: 2025-06-09T18:20:00
header:
  image: /assets/images/leetcode/managers-with-at-least-5-direct-reports.png
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
[Link](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT name FROM Employee
WHERE id IN (
  SELECT managerId FROM Employee
  GROUP BY managerId
  HAVING COUNT(*) >= 5
)
```

# 결과
[Link](https://leetcode.com/problems/managers-with-at-least-5-direct-reports/submissions/1658458659/){:target="_blank"}

# 설명
1. Employee 테이블에서 담당하고 있는 직원이 5명 이상인 매니저의 이름을 반환하는 문제이다.

2. Employee 테이블 내 매니저의 아이디가 5개 이상인 매니저 아이디만 서브 쿼리로 간추린다.

3. Employee 테이블에서 2번에서 간추린 아이디의 이름을 검색한다.