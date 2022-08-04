---
title: "Leetcode MySQL Sales Person"
excerpt: "Leetcode Sales Person MySQL 풀이"
last_modified_at: 2022-08-04T20:20:00
header:
  image: /assets/images/leetcode/sales-person.png
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
[Link](https://leetcode.com/problems/sales-person/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT name
FROM SalesPerson
WHERE sales_id NOT IN (
  SELECT Orders.sales_id
  FROM Orders
  JOIN Company ON Orders.com_id = Company.com_id
  WHERE Company.name = 'RED'
)
```

# 결과
[Link](https://leetcode.com/submissions/detail/764983577/){:target="_blank"}

# 설명
1. 'RED'라는 회사 외 주문이 없는 영업 사원의 이름을 찾는 문제이다.