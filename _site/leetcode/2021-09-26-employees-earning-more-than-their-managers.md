---
title: "Leetcode MySQL Employees Earning More Than Their Managers"
excerpt: "Leetcode Employees Earning More Than Their Managers MySQL 풀이"
last_modified_at: 2021-09-26T12:00:00
header:
  image: /assets/images/leetcode/employees-earning-more-than-their-managers.png
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
[Link](https://leetcode.com/problems/employees-earning-more-than-their-managers/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT Employee.Name as 'Employee'
FROM Employee
INNER JOIN Employee managers ON Employee.ManagerId = managers.Id
Where Employee.Salary > managers.Salary
```

# 결과
[Link](https://leetcode.com/submissions/detail/561027012/){:target="_blank"}

# 설명
1. 모든 직원과 매니저 정보가 저장된 Employee Table을 이용하여 매니저보다 급여가 많은 직원의 이름을 찾는 문제이다.

2. Employee를 다시 INNER JOIN을 걸어, ManagerId가 Null이 아닌 직원들에게 Manager 정보를 넣어 Salary를 비교하여 매니저보다 급여가 높은 직원의 Name만 출력한다.