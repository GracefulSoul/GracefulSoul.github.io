---
title: "Leetcode PostgreSQL Employee Bonus"
excerpt: "Leetcode Medium - 'Employee Bonus' 문제 PostgreSQL 풀이"
last_modified_at: 2025-06-05T21:55:00
header:
  image: /assets/images/leetcode/employee-bonus.png
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
[Link](https://leetcode.com/problems/employee-bonus/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT Employee.name, Bonus.bonus FROM Employee
LEFT OUTER JOIN Bonus ON Employee.empId = Bonus.empId
WHERE Bonus.bonus < 1000 OR Bonus.bonus IS NULL
```

# 결과
[Link](https://leetcode.com/problems/employee-bonus/submissions/1654702938/){:target="_blank"}

# 설명
1. 직원이 받은 보너스가 1000 미만인 직원의 이름과 보너스 금액을 반환하는 문제이다.

2. 보너스를 못받은 직원도 있으므로, Employee에 Bonus를 LEFT OUTER JOIN 후 bonus가 1000 미만이거나 null인 받지 못한 직원들만 조회한다.