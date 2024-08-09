---
title: "Leetcode PostgreSQL Article Views I"
excerpt: "Leetcode Article Views I PostgreSQL"
last_modified_at: 2024-08-09T18:50:00
header:
  image: /assets/images/leetcode/article-views-i.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - PostgreSQL

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/problems/article-views-i/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT DISTINCT viewer_id AS id FROM Views
WHERE viewer_id = author_id
ORDER BY viewer_id
```

# 결과
[Link](https://leetcode.com/problems/article-views-i/submissions/1349808113/){:target="_blank"}

# 설명
1. 자기가 작성한 기사를 읽은 작성자의 아이디를 오름차순 반환하는 문제이다.

2. viewer_id와 author_id가 동일한 데이터의 중복을 제거한 viewer_id를 오름차순으로 정렬한다.