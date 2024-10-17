---
title: "Leetcode MySQL Customers Who Never Order"
excerpt: "Leetcode - 'Customers Who Never Order MySQL 풀이"
last_modified_at: 2021-09-26T12:00:00
header:
  image: /assets/images/leetcode/customers-who-never-order.png
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
[Link](https://leetcode.com/problems/customers-who-never-order/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT Customers.Name AS 'Customers'
FROM Customers
LEFT OUTER JOIN Orders ON Customers.Id = Orders.CustomerId
WHERE Orders.Id IS NULL
```

# 결과
[Link](https://leetcode.com/submissions/detail/561030606/){:target="_blank"}

# 설명
1. Customers Table에서 한번도 주문하지 않은 고객을 찾는 문제이다.

2. Customers와 Orders Table을 LEFT OUTER JOIN을 이용하여 Orders의 Id가 Null인 대상의 Name만 출력하면 된다.