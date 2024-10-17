---
title: "Leetcode PostgreSQL Immediate Food Delivery II"
excerpt: "Leetcode Medium - 'Immediate Food Delivery II' 문제 PostgreSQL 풀이"
last_modified_at: 2024-08-25T14:50:00
header:
  image: /assets/images/leetcode/immediate-food-delivery-ii.png
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
[Link](https://leetcode.com/problems/immediate-food-delivery-ii/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT ROUND(AVG(CASE WHEN order_date = customer_pref_delivery_date THEN 1 ELSE 0 END) * 100, 2) AS immediate_percentage
FROM Delivery
WHERE (customer_id, order_date) IN (
  SELECT customer_id, MIN(order_date)
  FROM Delivery
  GROUP BY customer_id
)
```

# 결과
[Link](https://leetcode.com/problems/product-price-at-a-given-date/submissions/1367519463/){:target="_blank"}

# 설명
1. 고객별 첫 배송이 즉시 배송한 비율을 찾는 문제이다.
- 비율을 소수점 2자리까지 반환한다.

2. Delivery에서 고객 별 처음 배송을 찾기 위해서 customer_id를 기준으로 최소 order_date를 찾는다.

3. 찾은 배송일 중에서 order_date과 customer_pref_delivery_date이 동일한 경우에 대한 평균 값을 소수점 두 자리까지 계산한다.