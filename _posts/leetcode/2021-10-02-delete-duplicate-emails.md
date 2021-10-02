---
title: "Leetcode MySQL Delete Duplicate Emails"
excerpt: "Leetcode Delete Duplicate Emails MySQL 풀이"
last_modified_at: 2021-10-02T11:00:00
header:
  image: /assets/images/leetcode/delete-duplicate-emails.png
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
[Link](https://leetcode.com/problems/delete-duplicate-emails/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
DELETE Person FROM Person, Person temp
WHERE Person.Email = temp.Email
AND Person.Id > temp.Id
```

# 결과
[Link](https://leetcode.com/submissions/detail/564254778/){:target="_blank"}

# 설명
1. Person Table 내 각 중복된 Email 데이터들 중 Id가 가장 낮은 데이터들만 제외한 모든 데이터를 삭제하는 문제이다.

2. Person Table을 두 번 호출하여 EQUI JOIN으로 동일한 Email의 데이터를 연결한다.

3. p1의 Id가 p2의 Id보다 큰 p1의 데이터들을 모두 삭제한다.