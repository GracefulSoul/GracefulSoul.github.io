---
title: "Leetcode MySQL Department Highest Salary"
excerpt: "Leetcode Department Highest Salary MySQL 풀이"
last_modified_at: 2021-09-26T12:00:00
header:
  image: /assets/images/leetcode/department-highest-salary.png
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
[Link](https://leetcode.com/problems/department-highest-salary/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT Department.Name AS 'Department'
    , Employee.Name AS 'Employee'
    , Employee.Salary
FROM Employee
INNER JOIN Department ON Employee.DepartmentId = Department.Id
WHERE (Employee.DepartmentId, Employee.Salary) IN (
    SELECT DepartmentId, MAX(Salary)
    FROM Employee
    GROUP BY DepartmentId
)
```

# 결과
[Link](https://leetcode.com/submissions/detail/561042456/){:target="_blank"}

# 설명
1. Employee, Department Table을 이용하여 부서 별 가장 높은 급여를 받는 직원들을 찾는 문제이다.

2. Employee와 Department Table을 INNER JOIN 수행한다.

3. 서브 쿼리를 이용하여 DepartmentId 별 가장 높은 급여를 찾아 2번의 결과에서 해당 부서 별 급여를 받는 인원의 Department.Name, Employee.Name, Employee.Salary를 출력한다.