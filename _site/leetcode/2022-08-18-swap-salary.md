---
title: "Leetcode MySQL Swap Salary"
excerpt: "Leetcode Swap Salary MySQL 풀이"
last_modified_at: 2022-08-18T19:00:00
header:
  image: /assets/images/leetcode/swap-salary.png
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
[Link](https://leetcode.com/problems/swap-salary/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
UPDATE Salary
SET sex = CASE WHEN sex = 'm' THEN 'f' ELSE 'm' END
```

# 결과
[Link](https://leetcode.com/submissions/detail/776813154/){:target="_blank"}

# 설명
1. Salary 테이블 내 sex 컬럼의 값을 'm'은 'f'로, 'f'는 'm'으로 변환하는 쿼리를 만드는 문제이다.