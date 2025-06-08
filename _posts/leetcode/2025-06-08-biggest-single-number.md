---
title: "Leetcode PostgreSQL Biggest Single Number"
excerpt: "Leetcode Medium - 'Biggest Single Number' 문제 PostgreSQL 풀이"
last_modified_at: 2025-06-08T22:40:00
header:
  image: /assets/images/leetcode/biggest-single-number.png
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
[Link](https://leetcode.com/problems/biggest-single-number/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT MAX(num) AS num FROM (
  SELECT num
  FROM MyNumbers
  GROUP BY num
  HAVING COUNT(num) = 1
) AS UniqueNumbers
```

# 결과
[Link](https://leetcode.com/problems/biggest-single-number/submissions/1657689296/){:target="_blank"}

# 설명
1. MyNumbers 내 중복되지 않은 값 중 가장 큰 값을 찾는 문제이다.

2. 중복된 값을 제거하기 위해 num 기준으로 GROUP BY를 수행하고 발생 빈도가 1인 경우만 취합한 UniqueNumbers 서브 쿼리를 선언한다.

3. UniqueNumbers 내 가장 큰 num 값을 검색한다.