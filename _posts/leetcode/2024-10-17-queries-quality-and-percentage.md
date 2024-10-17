---
title: "Leetcode PostgreSQL Queries Quality and Percentage"
excerpt: "Leetcode Queries Quality and Percentage PostgreSQL"
last_modified_at: 2024-10-17T18:40:00
header:
  image: /assets/images/leetcode/queries-quality-and-percentage.png
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
[Link](https://leetcode.com/problems/queries-quality-and-percentage/){:target="_blank"}

# 코드
```sql
-- Write your MySQL query statement below
SELECT query_name
    , ROUND(AVG(rating::DECIMAL / position), 2) AS quality
    , ROUND(SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END)::DECIMAL / count(*) * 100, 2) AS poor_query_percentage
FROM Queries
WHERE query_name IS NOT NULL
GROUP BY query_name
```

# 결과
[Link](https://leetcode.com/problems/queries-quality-and-percentage/submissions/1425212687/){:target="_blank"}

# 설명
1. Queries 테이블에서 아래의 규칙의 값들을 query_name 기준으로 통계내는 문제이다.
- quality는 $\frac{rating}{position}$의 평균을 나타낸다.
- poor_query_percentage는 rating이 3 미만인 쿼리의 비율을 나타낸다.
- 각 결과는 임의 순서대로 반환하며, 통계 결과는 소수점 2자리까지 표현한다.

2. quality와 poor_query_percentage를 산출할 때 각 값은 int 형이므로, 소수점을 반환하기 위하여 분자를 DECIMAL 형으로 변경한다.

3. query_name이 nullable 필드이므로, NULL이 아닌 경우만 대상으로 한다.

4. query_name 기준으로 GROUP BY 수행하여 각 결과를 query_name 기준으로 통계내준다.