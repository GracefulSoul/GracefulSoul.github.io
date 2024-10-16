---
title: "Leetcode MySQL Actors and Directors Who Cooperated At Least Three Times"
excerpt: "Leetcode Actors and Directors Who Cooperated At Least Three Times MySQL 풀이"
last_modified_at: 2024-03-19T18:50:00
header:
  image: /assets/images/leetcode/actors-and-directors-who-cooperated-at-least-three-times.png
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
[Link](https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT actor_id, director_id
FROM ActorDirector
GROUP BY actor_id, director_id
HAVING COUNT(*) >= 3
```

# 결과
[Link](https://leetcode.com/problems/actors-and-directors-who-cooperated-at-least-three-times/submissions/1208048802/){:target="_blank"}

# 설명
1. ActorDirector 테이블에서 actor_id, director_id가 동일한 데이터가 3개 이상인 조합을 찾는 간단한 문제이다.