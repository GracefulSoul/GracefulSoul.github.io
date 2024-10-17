---
title: "Leetcode MySQL Customer Placing the Largest Number of Orders"
excerpt: "Leetcode - 'Customer Placing the Largest Number of Orders MySQL 풀이"
last_modified_at: 2022-07-19T19:00:00
header:
  image: /assets/images/leetcode/customer-placing-the-largest-number-of-orders.png
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
[Link](https://leetcode.com/problems/customer-placing-the-largest-number-of-orders/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT customer_number
FROM Orders
GROUP BY customer_number
ORDER BY COUNT(order_number) DESC
LIMIT 1
```

# 결과
[Link](https://leetcode.com/submissions/detail/751021132/){:target="_blank"}

# 설명
1. Orders Table의 데이터 중 주문이 가장 많은 customer_number를 찾는 문제이다.