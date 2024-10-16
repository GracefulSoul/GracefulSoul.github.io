---
title: "Leetcode MySQL Find Customer Referee"
excerpt: "Leetcode Find Customer Referee MySQL 풀이"
last_modified_at: 2022-07-19T19:00:00
header:
  image: /assets/images/leetcode/find-customer-referee.png
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
[Link](https://leetcode.com/problems/find-customer-referee/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT name FROM Customer
WHERE referee_id != 2 OR referee_id IS NULL
```

# 결과
[Link](https://leetcode.com/submissions/detail/751013705/){:target="_blank"}

# 설명
1. Customer Table의 referee_id 값이 2가 아닌 name을 출력하는 문제이다.
- NULL의 경우, "!=" 부등호로 비교가 되지 않으므로 IS NULL을 추가해야 한다.