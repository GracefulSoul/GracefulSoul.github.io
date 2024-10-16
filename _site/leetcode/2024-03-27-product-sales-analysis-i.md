---
title: "Leetcode PostgreSQL Product Sales Analysis I"
excerpt: "Leetcode Product Sales Analysis I PostgreSQL"
last_modified_at: 2024-03-27T19:00:00
header:
  image: /assets/images/leetcode/product-sales-analysis-i.png
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
[Link](https://leetcode.com/problems/product-sales-analysis-i/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT Product.product_name, Sales.year, Sales.price
FROM Sales
JOIN Product ON Product.product_id = Sales.product_id
```

# 결과
[Link](https://leetcode.com/problems/product-sales-analysis-i/submissions/1215290878/){:target="_blank"}

# 설명
1. Sales 테이블의 product_id를 이용하여 Product의 이름을 가져와 product_name, year, price 순으로 필드를 보여주는 문제이다.