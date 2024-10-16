---
title: "Leetcode MySQL Customers Who Bought All Products"
excerpt: "Leetcode Customers Who Bought All Products MySQL 풀이"
last_modified_at: 2024-03-15T10:00:00
header:
  image: /assets/images/leetcode/customers-who-bought-all-products.png
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
[Link](https://leetcode.com/problems/customers-who-bought-all-products/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT customer_id FROM Customer
GROUP BY customer_id
HAVING COUNT(distinct product_key) = (SELECT COUNT(product_key) FROM Product)
```

# 결과
[Link](https://leetcode.com/problems/customers-who-bought-all-products/submissions/1203956871/){:target="_blank"}

# 설명
1. Product 테이블에 등록된 모든 품목을 구매한 customer_id를 Customer 테이블에서 찾는 문제이다.

2. Customer 테이블의 customer_id 기준으로 GROUP BY 수행할 때 아래를 조건으로 수행한다.
- GROUP BY 되는 customer_id의 갯수가 Product 테이블의 품목 갯수와 동일한지 여부를 HAVING 조건으로 수행한다.