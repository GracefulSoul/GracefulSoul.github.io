---
title: "Leetcode PostgreSQL Students and Examinations"
excerpt: "Leetcode Medium - 'Students and Examinations' 문제 PostgreSQL 풀이"
last_modified_at: 2025-07-31T18:00:00
header:
  image: /assets/images/leetcode/students-and-examinations.png
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
[Link](https://leetcode.com/problems/students-and-examinations/){:target="_blank"}

# 코드
```sql
-- Write your PostgreSQL query statement below
SELECT Students.student_id
  , Students.student_name
  , Subjects.subject_name
  , COUNT(Examinations.student_id) AS attended_exams
FROM Students
CROSS JOIN Subjects
LEFT OUTER JOIN Examinations ON Students.student_id = Examinations.student_id AND Subjects.subject_name = Examinations.subject_name
GROUP BY Students.student_id, Students.student_name, Subjects.subject_name
ORDER BY Students.student_id, Subjects.subject_name
```

# 결과
[Link](https://leetcode.com/problems/students-and-examinations/submissions/1718100725/){:target="_blank"}

# 설명
1. 아래 테이블들을 이용하여 학생의 각 과목 별 시험을 본 횟수를 구하는 문제이다.
- Students 테이블은 학생 정보(student_id, student_name)가 저장된다.
- Subjects 테이블은 과목 정보(subject_name)가 저장된다.
- Examinations 테이블은 학생 별 시험을 치룬 정보(student_id, subject_name)가 저장된다.

2. Students 테이블 과 Subjects 테이블을 CROSS JOIN하여 학생과 전과목 정보를 1:1로 이어준다.

3. Examinations을 Students 테이블의 student_id와 Subjects 테이블의 subject_name를 각 필드 기준으로 OUTER 조인을 함으로 학생 별 시험본 과목을 연결해준다.

4. COUNT 함수와 GROUP BY 구문을 통해 이용하여 3번의 OUTER 조인을 통해 학생 별 시험을 본 과목의 갯수를 계산해준다.

5. ORDER BY 구문으로 Students 테이블의 student_id, Subjects 테이블의 subject_name 기준의 오름차순으로 정렬해준다.