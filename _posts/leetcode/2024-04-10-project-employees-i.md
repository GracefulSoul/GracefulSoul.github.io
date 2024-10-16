---
title: "Leetcode PostgreSQL Project Employees I"
excerpt: "Leetcode Project Employees I PostgreSQL"
last_modified_at: 2024-04-10T09:30:00
header:
  image: /assets/images/leetcode/project-employees-i.png
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
[Link](https://leetcode.com/problems/project-employees-i/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT Project.project_id
	, ROUND(AVG(Employee.experience_years), 2) AS average_years
FROM Project
JOIN Employee ON Employee.employee_id = Project.employee_id
GROUP BY Project.project_id
```

# 결과
[Link](https://leetcode.com/problems/project-employees-i/submissions/1228103161/){:target="_blank"}

# 설명
1. Project 별 Employee의 평균 경력을 소수점 2자리까지 계산하는 문제이다.