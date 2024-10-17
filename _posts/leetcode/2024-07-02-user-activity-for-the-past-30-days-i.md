---
title: "Leetcode PostgreSQL User Activity for the Past 30 Days I"
excerpt: "Leetcode Easy - 'User Activity for the Past 30 Days I' 문제 PostgreSQL 풀이"
last_modified_at: 2024-07-02T18:30:00
header:
  image: /assets/images/leetcode/user-activity-for-the-past-30-days-i.png
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
[Link](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT activity_date AS day, COUNT(DISTINCT user_id) AS active_users FROM Activity
WHERE activity_date > '2019-07-27'::date - INTERVAL '30 days'
AND activity_date <= '2019-07-27'
GROUP BY activity_date
```

# 결과
[Link](https://leetcode.com/problems/user-activity-for-the-past-30-days-i/submissions/1306810156/){:target="_blank"}

# 설명
1. 2019-07-27일 까지 최근 30일 동안 활성화 유저를 계산하는 문제이다.

2. 2019-07-27일에서 30일을 차감한 날자 초과부터 해당 날 이전까지의 Activity 테이블 내 데이터가 문제의 활성 유저를 구하는 조건이 된다.

3. 활성화 유저는 Activity 테이블에서 'open_session'과 'end_session'의 로그의 시간동안 세션이 유지되며 하루에 한 번의 활동을 수행해야 세션이 유지되므로, user_id가 중복되지 않은 일자까지가 활성 유저의 수가 된다.