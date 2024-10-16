---
title: "Leetcode PostgreSQL Monthly Transactions I"
excerpt: "Leetcode Monthly Transactions I PostgreSQL"
last_modified_at: 2024-09-26T19:20:00
header:
  image: /assets/images/leetcode/monthly-transactions-i.png
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
[Link](https://leetcode.com/problems/monthly-transactions-i/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT
  TO_CHAR(trans_date, 'YYYY-MM') AS month,
  country,
  COUNT(*) AS trans_count,
  SUM(CASE WHEN state = 'approved' THEN 1 ELSE 0 END) AS approved_count,
  SUM(amount) AS trans_total_amount,
  SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM Transactions
GROUP BY TO_CHAR(trans_date, 'YYYY-MM'), country
```

# 결과
[Link](https://leetcode.com/problems/monthly-transactions-i/submissions/1402793914/){:target="_blank"}

# 설명
1. Transactions 테이블에서 월, 지역 별 아래의 산술 지표를 구하는 문제이다.
- trans_count는 두 조건 내 해당하는 데이터의 갯수이다.
- approved_count는 두 조건 내 해당하는 데이터 중 state가 approved인 갯수이다.
  - state가 approved인 값을 1, 나머지를 0으로 설정하였기 때문에 SUM인 합계를 활용하여 갯수를 계산한다.
- trans_total_amount는 두 조건 내 해당하는 amount의 합이다.
- approved_total_amount는 두 조건 내 해당하는 데이터 중 state가 approved인 amount의 합이다.