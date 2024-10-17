---
title: "Leetcode MySQL Rising Temperature"
excerpt: "Leetcode - 'Rising Temperature MySQL 풀이"
last_modified_at: 2021-10-02T11:00:00
header:
  image: /assets/images/leetcode/rising-temperature.png
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
[Link](https://leetcode.com/problems/rising-temperature/){:target="_blank"}

# 코드
```sql
# Write your MySQL query statement below
SELECT Weather.Id FROM Weather
INNER JOIN Weather temp ON TO_DAYS(Weather.RecordDate) - TO_DAYS(temp.RecordDate) = 1
WHERE Weather.Temperature > temp.Temperature
```

# 결과
[Link](https://leetcode.com/submissions/detail/564256620/){:target="_blank"}

# 설명
1. Weather Table에서 이전 날보다 날씨가 더 올라간 데이터의 Id를 출력하는 문제이다.

2. Weather Table을 두 번 호출하여 INNER JOIN으로 Weather.RecordDate를 TO_DAYS 함수로 형 변환한 값과 temp.RecordDate를 TO_DAYS 함수로 형변환 한 값의 차이가 1인 경우를 조인한다.

3. Weather.Temperature가 temp.Temperature보다 큰 데이터들의 Id를 출력한다.