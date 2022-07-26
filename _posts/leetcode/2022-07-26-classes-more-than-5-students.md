---
title: "Leetcode MySQL Big Countries"
excerpt: "Leetcode Big Countries MySQL 풀이"
last_modified_at: 2022-07-26T19:30:00
header:
  image: /assets/images/leetcode/classes-more-than-5-students.png
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
[Link](https://leetcode.com/problems/classes-more-than-5-students/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(student) > 4
```

# 결과
[Link](https://leetcode.com/submissions/detail/757135715/){:target="_blank"}

# 설명
1. Courses Table 의 수강생이 5명 이상인 class를 찾는 문제이다.