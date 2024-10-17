---
title: "Leetcode PostgreSQL Last Person to Fit in the Bus"
excerpt: "Leetcode Medium - 'Last Person to Fit in the Bus' 문제 PostgreSQL 풀이"
last_modified_at: 2024-10-09T12:20:00
header:
  image: /assets/images/leetcode/last-person-to-fit-in-the-bus.png
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
[Link](https://leetcode.com/problems/last-person-to-fit-in-the-bus/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT person_name
FROM (
  SELECT person_name, weight, turn, SUM(weight) OVER (ORDER BY turn) AS sum
  FROM Queue
) AS Queue
WHERE sum <= 1000
ORDER BY turn DESC 
LIMIT 1
```

# 결과
[Link](https://leetcode.com/problems/last-person-to-fit-in-the-bus/submissions/1416523839/){:target="_blank"}

# 설명
1. Queue 테이블의 사람들이 turn 순서대로 버스를 탑승할 때, weight의 합산이 1000kg 초과하지 않고 탑승할 수 있는 마지막 person_name을 탐색하는 문제이다.

2. 서브 쿼리로 weight의 합계를 turn 순서대로 수행한다.

3. turn 순서대로 내림차순 정렬하여 sum이 1000 이하인 마지막 탑승한 한 사람을 탐색한다.