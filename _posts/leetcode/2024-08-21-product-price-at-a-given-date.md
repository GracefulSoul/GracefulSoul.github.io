---
title: "Leetcode PostgreSQL Product Price at a Given Date"
excerpt: "Leetcode Medium - 'Product Price at a Given Date' 문제 PostgreSQL 풀이"
last_modified_at: 2024-08-21T18:50:00
header:
  image: /assets/images/leetcode/product-price-at-a-given-date.png
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
[Link](https://leetcode.com/problems/product-price-at-a-given-date/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT Products.product_id, COALESCE(MIN(product_price.new_price), 10) AS price
FROM (
  SELECT DISTINCT product_id FROM Products
) AS Products
LEFT OUTER JOIN (
  SELECT product_id, new_price FROM Products
  WHERE (product_id, change_date) IN (
    SELECT product_id, MAX(change_date) AS date FROM Products
    WHERE change_date <= '2019-08-16'
    GROUP BY product_id
  )
) AS product_price ON Products.product_id = product_price.product_id
GROUP BY Products.product_id
```

# 결과
[Link](https://leetcode.com/problems/product-price-at-a-given-date/submissions/1363322058/){:target="_blank"}

# 설명
1. 제품별 가격 변경 이력이 저장된 Products를 이용하여 '2019-08-16'일 기준으로 각 제품의 가격을 구하는 문제이다.
- 각 제품의 초기 가격은 10이라고 가정한다.

2. 각 제품 이력 별 고유한 product_id를 먼저 구한다.

3. 제품 별 '2019-08-16' 이전까지의 제품 별 마지막 가격 변경 이력을 구한다.
- Products 테이블에서 '2019-08-16' 이전까지 product_id 별 가장 최근 변경 이력을 구한다.
- 위의 product_id 별 가장 최근 변경 이력에 대한 가격을 다시 Products에서 검색한다.

4. 2번과 3번을 통해서 구해진 두 값을 조인하되, 가격 정보가 없는 경우 10을 기본 값으로 설정하여 검색을 수행한다.