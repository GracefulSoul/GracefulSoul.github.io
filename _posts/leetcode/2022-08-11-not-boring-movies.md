---
title: "Leetcode MySQL Not Boring Movies"
excerpt: "Leetcode Not Boring Movies MySQL 풀이"
last_modified_at: 2022-08-11T19:20:00
header:
  image: /assets/images/leetcode/not-boring-movies.png
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
[Link](https://leetcode.com/problems/not-boring-movies/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT *
FROM Cinema
WHERE id % 2
AND description NOT LIKE '%boring%'
ORDER BY rating DESC
```

# 결과
[Link](https://leetcode.com/submissions/detail/770972276/){:target="_blank"}

# 설명
1. Cinema 테이블 내 id가 홀수이면서 지루한(boring)하다고 남기지 않은 값들을 찾는 문제이다.