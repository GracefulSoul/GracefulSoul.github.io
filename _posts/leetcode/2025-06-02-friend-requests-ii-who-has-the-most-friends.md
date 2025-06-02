---
title: "Leetcode PostgreSQL Friend Requests II: Who Has the Most Friends"
excerpt: "Leetcode Medium - 'Friend Requests II: Who Has the Most Friends' 문제 PostgreSQL 풀이"
last_modified_at: 2025-06-02T21:15:00
header:
  image: /assets/images/leetcode/friend-requests-ii-who-has-the-most-friends.png
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
[Link](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
WITH ids AS (
  SELECT requester_id AS id FROM RequestAccepted
  UNION ALL
  SELECT accepter_id AS id FROM RequestAccepted
)
SELECT id, COUNT(*) AS num
FROM ids
GROUP BY id
ORDER BY num DESC
LIMIT 1
```

# 결과
[Link](https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/submissions/1651656888/){:target="_blank"}

# 설명
1. 친구 요청에 대한 데이터가 담긴 RequestAccepted를 이용하여 친구가 가장 많은 친구의 아이디와 보유한 친구의 수를 반환하는 문제이다.

2. 요청한 아이디인 requester_id와 수학한 아이디인 accepter_id의 값을 한 컬럼으로 모은 서브 쿼리이다.
- 친구를 요청한 계정과 수락한 계정은 서로 친구 관계이므로, 친구 수를 하나의 컬럼으로 모은다.

3. 2번에서 정의한 ids의 id를 기준으로 갯수가 가장 많은 하나의 행만 가져온다.