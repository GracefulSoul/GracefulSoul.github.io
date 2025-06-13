---
title: "Leetcode PostgreSQL Triangle Judgement"
excerpt: "Leetcode Medium - 'Triangle Judgement' 문제 PostgreSQL 풀이"
last_modified_at: 2025-06-13T19:25:00
header:
  image: /assets/images/leetcode/triangle-judgement.png
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
[Link](https://leetcode.com/problems/triangle-judgement/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT x, y, z, CASE WHEN x + y > z AND x + z > y AND y + z > x THEN 'Yes' ELSE 'No' END AS triangle
FROM Triangle
```

# 결과
[Link](https://leetcode.com/problems/triangle-judgement/submissions/1662823979/){:target="_blank"}

# 설명
1. 삼각형 세 변의 길이인 x, y, z가 저장된 Triangle 테이블을 이용하여 삼각형을 만들 수 있는지 여부를 같이 조회하는 문제이다.

2. x, y, z 기본 세 값과 triangle 컬럼 값에 [삼각 부등식](https://en.wikipedia.org/wiki/Triangle_inequality){:target="_blank"}을 만족하여 삼각형을 만들 수 있으면 'Yes'를, 아니면 'No'를 넣어준다.