---
title: "Leetcode MySQL Nth Highest Salary"
excerpt: "Leetcode - 'Nth Highest Salary MySQL 풀이"
last_modified_at: 2021-09-25T12:00:00
header:
  image: /assets/images/leetcode/nth-highest-salary.png
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
[Link](https://leetcode.com/problems/nth-highest-salary/){:target="_blank"}

# 코드
```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT
BEGIN
DECLARE Num int;
SET Num = N - 1;
  RETURN (
      # Write your MySQL query statement below.
      SELECT DISTINCT Salary FROM Employee ORDER BY Salary DESC LIMIT Num, 1
  );
END
```

# 결과
[Link](https://leetcode.com/submissions/detail/560504372/){:target="_blank"}

# 설명
1. Employee Table의 N번째 Salary 값을 가져오는 getNthHighestSalary FUNCTION을 완성하는 문제이다.

2. INPUT PARAMETER인 N을 이용하여 Num 변수에 N - 1을 넣어준다.

3. Employee Table을 Salary 기준으로 정렬하여 DISTCINT된 Salary의 값을 LIMIT을 이용하여 Num번째 값 이후 1개를 가져오면 된다.