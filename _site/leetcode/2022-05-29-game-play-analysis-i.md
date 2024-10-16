---
title: "Leetcode MySQL Game Play Analysis I"
excerpt: "Leetcode Game Play Analysis I MySQL 풀이"
last_modified_at: 2022-05-29T06:00:00
header:
  image: /assets/images/leetcode/game-play-analysis-i.png
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
[Link](https://leetcode.com/problems/game-play-analysis-i/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT player_id, MIN(event_date) AS first_login FROM Activity
GROUP BY player_id
```

# 결과
[Link](https://leetcode.com/submissions/detail/709290184/){:target="_blank"}

# 설명
1. Activity Table의 player_id 별 최초 로그인 날자를 구하는 문제이다.