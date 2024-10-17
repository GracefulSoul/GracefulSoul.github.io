---
title: "Leetcode PostgreSQL Market Analysis I"
excerpt: "Leetcode Medium - 'Market Analysis I' 문제 PostgreSQL 풀이"
last_modified_at: 2024-08-13T19:20:00
header:
  image: /assets/images/leetcode/market-analysis-i.png
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
[Link](https://leetcode.com/problems/market-analysis-i/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT Users.user_id AS buyer_id
	, Users.join_date
	, COUNT(Orders.order_id) AS orders_in_2019
FROM Users
LEFT OUTER JOIN Orders ON Users.user_id = Orders.buyer_id AND DATE_PART('year', Orders.order_date) = '2019'
GROUP BY Users.user_id
	, Users.join_date
```

# 결과
[Link](https://leetcode.com/problems/market-analysis-i/submissions/1354157343/){:target="_blank"}

# 설명
1. 사용자 별 가입 일자와 2019년도 주문 횟수를 조회하는 문제이다.

2. Orders 테이블의 이력이 없을 수 있으므로 LEFT OUTER JOIN을 사용하되, Users 테이블의 user_id와 Orders 테이블의 구매자 정보인 buyer_id가 동일하면서 2019년도 주문인 경우만 대상으로 한다.

3. Users 테이블의 사용자 기반으로, user_id를 buyer_id로 join_date 기준으로 Orders 테이블의 데이터 갯수를 계산해준다.
