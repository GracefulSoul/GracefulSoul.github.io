---
title: "Leetcode MySQL Duplicate Emails"
excerpt: "Leetcode - 'Duplicate Emails MySQL 풀이"
last_modified_at: 2021-09-26T12:00:00
header:
  image: /assets/images/leetcode/duplicate-emails.png
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
[Link](https://leetcode.com/problems/duplicate-emails/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT Email FROM Person
GROUP BY Email
HAVING COUNT(*) > 1
```

# 결과
[Link](https://leetcode.com/submissions/detail/561028785/){:target="_blank"}

# 설명
1. Person Table에서 중복 사용된 Email을 찾는 문제이다.

2. 간단한 집계함수를 이용하여 Email이 중복된 개수가 1개 초과인 Email만 출력한다.