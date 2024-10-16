---
title: "Leetcode MySQL Combine Two Tables"
excerpt: "Leetcode Combine Two Tables MySQL 풀이"
last_modified_at: 2021-09-25T12:00:00
header:
  image: /assets/images/leetcode/combine-two-tables.png
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
[Link](https://leetcode.com/problems/combine-two-tables/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT Person.FirstName, Person.LastName, Address.City, Address.State FROM Person
LEFT OUTER JOIN Address ON Person.PersonId = Address.PersonId
```

# 결과
[Link](https://leetcode.com/submissions/detail/560496846/){:target="_blank"}

# 설명
1. Person Table과 Address Table을 JOIN하는 기초적인 문제이다.