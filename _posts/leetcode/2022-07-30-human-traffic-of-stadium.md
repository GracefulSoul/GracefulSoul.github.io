---
title: "Leetcode MySQL Human Traffic of Stadium"
excerpt: "Leetcode Human Traffic of Stadium MySQL 풀이"
last_modified_at: 2022-07-30T12:30:00
header:
  image: /assets/images/leetcode/human-traffic-of-stadium.png
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
[Link](https://leetcode.com/problems/human-traffic-of-stadium/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
WITH tab AS (
  SELECT id, visit_date, people, id - ROW_NUMBER() OVER(ORDER BY id) AS group_id
  FROM Stadium
  WHERE people >= 100 
)
SELECT id, visit_date, people
from tab 
WHERE group_id in (
  SELECT group_id
  FROM tab
  GROUP BY group_id
  HAVING COUNT(*) >= 3
)
```

# 결과
[Link](https://leetcode.com/submissions/detail/760995664/){:target="_blank"}

# 설명
1. Stadium Table의 people이 100 이상이고 연속한 3일 이상 해당 조건을 만족하는 경우의 데이터를 찾는 문제이다.