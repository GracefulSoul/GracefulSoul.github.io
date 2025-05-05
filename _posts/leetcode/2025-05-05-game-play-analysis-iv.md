---
title: "Leetcode PostgreSQL Game Play Analysis IV"
excerpt: "Leetcode Medium - 'Game Play Analysis IV' 문제 PostgreSQL 풀이"
last_modified_at: 2025-05-05T11:45:00
header:
  image: /assets/images/leetcode/game-play-analysis-iv.png
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
[Link](https://leetcode.com/problems/game-play-analysis-iv/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT ROUND(COUNT(Activity2.player_id)::numeric / COUNT(Activity1.player_id), 2) AS fraction
FROM (
	SELECT player_id, MIN(event_date) AS first_login
	FROM Activity
	GROUP BY player_id
) Activity1
LEFT JOIN Activity Activity2 ON Activity1.player_id = Activity2.player_id AND Activity1.first_login = Activity2.event_date - 1
```

# 결과
[Link](https://leetcode.com/problems/game-play-analysis-iv/submissions/1625731740/){:target="_blank"}

# 설명
1. 게임 활동 이력이 담긴 Activity 테이블을 이용하여 첫 로그인 이후 이틀 연속 접속한 사용자의 비율을 소수점 두 자리까지 반올림하여 계산하는 문제이다.

2. 사용자 별 처음 로그인한 시간을 frist_login으로 담아 Activity1을 정의한다.

3. Activity 테이블을 Activity2로 정의하여 Activity1과 player_id와 first_login과 event_date의 전날이 동일한 계정을 기준으로 LEFT OUTER JOIN을 수행하여 연속 접속한 정보를 넣어준다.

4. Activity2의 player_id인 이틀 연속 접속한 사용자의 수를 실수형으로 변환하여 Activity1의 player_id인 전체 사용자 수로 나누어 소수점 두 자리까지 반올림하여 비율을 계산한다.
