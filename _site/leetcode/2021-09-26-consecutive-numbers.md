---
title: "Leetcode MySQL Consecutive Numbers"
excerpt: "Leetcode Consecutive Numbers MySQL 풀이"
last_modified_at: 2021-09-26T12:00:00
header:
  image: /assets/images/leetcode/consecutive-numbers.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - MySQL

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/problems/consecutive-numbers/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT DISTINCT Num AS ConsecutiveNums
FROM Logs l1
WHERE (l1.Id + 1, Num) IN (SELECT * FROM Logs)
AND (l1.Id + 2, Num) IN (SELECT * FROM Logs)
#WHERE EXISTS (
#    SELECT 1 FROM Logs l2
#    WHERE l2.Id = l1.Id + 1 AND l1.Num = l2.Num
#)
#AND EXISTS (
#    SELECT 1 FROM Logs l2
#    WHERE l2.Id = l1.Id + 2 AND l1.Num = l2.Num
#)
```

# 결과
[Link](https://leetcode.com/submissions/detail/561022135/){:target="_blank"}

# 설명
1. Logs Table에서 연속된 Id에 동일한 Num이 들어가 있는 모든 Id를 반환하는 문제이다.

2. Logs Table에 $Id + 1$과 Num, $Id + 2$와 Num이 존재하는지를 검증하면 된다.
- WHERE 조건문의 IN과 EXISTS는 비슷한 용도로 사용하지만, 일반적으로 데이터가 많을수록 EXISTS가 적을수록 IN이 효율적이다.