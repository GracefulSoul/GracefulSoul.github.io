---
title: "Leetcode MySQL Rank Scores"
excerpt: "Leetcode Rank Scores MySQL 풀이"
last_modified_at: 2021-09-25T12:00:00
header:
  image: /assets/images/leetcode/rank-scores.png
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
[Link](https://leetcode.com/problems/rank-scores/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT s1.Score, COUNT(DISTINCT s2.SCORE) AS 'Rank'
FROM Scores s1
INNER JOIN Scores s2 ON s1.Score <= s2.Score
GROUP BY s1.Id
ORDER BY s1.Score DESC
```

# 결과
[Link](https://leetcode.com/submissions/detail/560502120/){:target="_blank"}

# 설명
1. Scores Table에서 Score 별 Rank를 메겨서 높은 순서대로 정렬하는 문제이다.

2. Scores Table을 두 번 호출하여 서로 INNER JOIN한다.

3. s1.Score 보다 작은 s2.Score를 JOIN 걸어 RANK를 메긴다.

4. 집계함수를 사용하므로, s1.Id으로 GROUP하고 s1.Score를 DESC로 정렬한다.