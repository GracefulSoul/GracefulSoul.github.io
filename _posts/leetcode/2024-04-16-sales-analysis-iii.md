---
title: "Leetcode PostgreSQL Sales Analysis III"
excerpt: "Leetcode Sales Analysis III PostgreSQL"
last_modified_at: 2024-04-16T18:50:00
header:
  image: /assets/images/leetcode/sales-analysis-iii.png
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
[Link](https://leetcode.com/problems/sales-analysis-iii/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT Product.product_id, Product.product_name
FROM Product
WHERE EXISTS (
	SELECT 1 FROM Sales
	WHERE Sales.sale_date BETWEEN '2019-01-01' AND '2019-03-31'
	AND Sales.product_id = Product.product_id
)
AND NOT EXISTS (
	SELECT 1 FROM Sales
	WHERE Sales.sale_date NOT BETWEEN '2019-01-01' AND '2019-03-31'
	AND Sales.product_id = Product.product_id
)
```

# 결과
[Link](https://leetcode.com/problems/project-employees-i/submissions/1228103161/){:target="_blank"}

# 설명
1. Product 중 2019년 1분기(2019-01-01 ~ 2019-03-31)에만 판매된 품목의 product_id와 product_name을 찾는 문제이다.