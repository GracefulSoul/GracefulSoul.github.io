---
title: "Leetcode PostgreSQL Product Sales Analysis III"
excerpt: "Leetcode Product Sales Analysis III PostgreSQL"
last_modified_at: 2024-04-01T19:30:00
header:
  image: /assets/images/leetcode/product-sales-analysis-iii.png
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
[Link](https://leetcode.com/problems/product-sales-analysis-iii/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT product_id, year AS first_year, quantity, price
FROM Sales
WHERE (product_id, year) IN (
    SELECT product_id, MIN(year)
    FROM Sales
    GROUP BY product_id
)
```

# 결과
[Link](https://leetcode.com/problems/product-sales-analysis-iii/submissions/1219982858/){:target="_blank"}

# 설명
1. Sales 테이블은 판매한 이력을 가진 테이블로, 각 물품별로 첫 해에 팔린 모든 행의 product id, year, quantity, price 필드만 반환하는 문제이다.

2. 문제의 목표는 product_id 별 가장 작은 년도에 팔린 데이터를 가져와야 하므로, Sales의 데이터를 product_id와 year의 최솟값을 간추려 Sales 테이블의 앞의 값의 데이터들만 가져온다.