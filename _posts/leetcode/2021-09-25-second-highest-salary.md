---
title: "Leetcode MySQL Second Highest Salary"
excerpt: "Leetcode Second Highest Salary MySQL 풀이"
last_modified_at: 2021-09-25T12:00:00
header:
  image: /assets/images/leetcode/second-highest-salary.png
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
[Link](https://leetcode.com/problems/second-highest-salary/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT MAX(Salary) AS 'SecondHighestSalary'
FROM Employee
WHERE Salary NOT IN (
    SELECT MAX(Salary) FROM Employee
)
```

# 결과
[Link](https://leetcode.com/submissions/detail/560501331/){:target="_blank"}

# 설명
1. Employee Table의 두 번째 높은 Salary 값을 구하는 문제이다.

2. Employee Table의 가장 큰 Salary 값을 제외한 가장 큰 Salary를 구하면 된다.