---
title: "Leetcode MySQL Big Countries"
excerpt: "Leetcode Big Countries MySQL 풀이"
last_modified_at: 2022-07-26T19:30:00
header:
  image: /assets/images/leetcode/big-countries.png
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
[Link](https://leetcode.com/problems/big-countries/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000
```

# 결과
[Link](https://leetcode.com/submissions/detail/757131376/){:target="_blank"}

# 설명
1. World Table의 area가 $3000000 km^2$ 이상이거나 population 이 25000000 이상인 경우의 나라을 구하는 문제이다.