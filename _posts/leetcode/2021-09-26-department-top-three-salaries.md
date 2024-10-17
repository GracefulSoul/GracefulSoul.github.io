---
title: "Leetcode MySQL Department Top Three Salaries"
excerpt: "Leetcode - 'Department Top Three Salaries MySQL 풀이"
last_modified_at: 2021-09-26T12:00:00
header:
  image: /assets/images/leetcode/department-top-three-salaries.png
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
[Link](https://leetcode.com/problems/department-top-three-salaries/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT Department.Name AS 'Department'
    , Employee.Name AS 'Employee'
    , Employee.Salary
FROM Employee
INNER JOIN Department ON Employee.DepartmentId = Department.Id
LEFT OUTER JOIN Employee temp ON Department.Id = temp.DepartmentId AND Employee.Salary < temp.Salary
GROUP BY Department.Name
    , Employee.Name
    , Employee.Salary
HAVING COUNT(DISTINCT temp.Salary) < 3
```

# 결과
[Link](https://leetcode.com/submissions/detail/561049407/){:target="_blank"}

# 설명
1. Employee, Department Table을 이용하여 부서 별 가장 높은 급여를 받는 3명의 직원들을 찾는 문제이다.

2. Employee와 Department Table을 INNER JOIN 수행한다.

3. 비교를 위한 Employee Table을 temp란 별칭으로 LEFT OUTER JOIN을 이용하여 Department Table의 Id가 동일하고 Employee Table의 Salary보다 큰 값을 넣어준다.

4. 그룹 함수를 이용하여 중복되지 않은 temp.Salary가 3개 미만인 개수만 대상으로 Department.Name, Employee.Name, Employee.Salary을 출력한다.
- Employee와 Department Table을 JOIN된 결과에서 LEFT OUTER JOIN으로 Employee를 급여 기준으로 걸었기 때문에, 급여가 높은 인원만큼의 Row가 추가 생성된다.
- 이 Row를 기준으로 COUNT를 세서 3개 미만인 경우만 출력되게 한 것이다.