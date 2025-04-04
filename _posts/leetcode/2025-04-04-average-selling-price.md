---
title: "Leetcode PostgreSQL Average Selling Price"
excerpt: "Leetcode Medium - 'Average Selling Price' 문제 PostgreSQL 풀이"
last_modified_at: 2025-04-04T18:30:00
header:
  image: /assets/images/leetcode/average-selling-price.png
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
[Link](https://leetcode.com/problems/average-selling-price/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT Prices.product_id
    , ROUND(COALESCE(SUM(Prices.price * UnitsSold.units), 0)::NUMERIC / COALESCE(SUM(UnitsSold.units), 1), 2) AS average_price
FROM Prices
LEFT OUTER JOIN UnitsSold ON Prices.product_id = UnitsSold.product_id AND  Prices.start_date <= UnitsSold.purchase_date AND UnitsSold.purchase_date <= Prices.end_date
GROUP BY Prices.product_id
```

# 결과
[Link](https://leetcode.com/problems/average-selling-price/submissions/1596416015/){:target="_blank"}

# 설명
1. 일자별 가격을 저장한 Prices를 이용하여 판매 기록인 UnitsSold의 품목 별 평균 판매가를 구하는 문제이다.

2. Prices에 UnitsSold 테이블을 LEFT OUTER JOIN 을 수행한다.
- 이 때 두 테이블의 product_id는 동일해야 하며, UnitsSold 테이블의 purchase_date는 Prices 테이블의 start_date 부터 end_date 이하여야 한다.

3. Prices 테이블의 product_id 기준으로 GROUP BY 수행하면서, 아래의 두 값을 나눈 후 소수점 2자리 반올림 처리한 평균 판매가를 구해준다.
- Prices 테이블의 price의 값과 UnitsSold 테이블의 units 갯수를 곱한 값이 NULL이면 0, 아니면 곱한 값에 소수점을 포함한 NUMERIC으로 변환한 값.
- UnitsSold 테이블의 units 갯수의 합이 null이면 1로, 아니면 해당 값.