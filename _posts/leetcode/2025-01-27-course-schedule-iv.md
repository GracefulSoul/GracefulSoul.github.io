---
title: "Leetcode Java Course Schedule IV"
excerpt: "Leetcode - 'Course Schedule IV' 문제 Java 풀이"
last_modified_at: 2025-01-27T12:30:00
header:
  image: /assets/images/leetcode/course-schedule-iv.png
categories:
  - Leetcode
tags:
  - Programming
  - Leetcode
  - Java

toc: true
toc_ads: true
toc_sticky: true
use_math: true
---
# 문제
[Link](https://leetcode.com/problems/course-schedule-iv/){:target="_blank"}

# 코드
```java
class Solution {

  public List<Boolean> checkIfPrerequisite(int numCourses, int[][] prerequisites, int[][] queries) {
    boolean[][] connected = new boolean[numCourses][numCourses];
    for (int[] prerequisite : prerequisites) {
      connected[prerequisite[0]][prerequisite[1]] = true;
    }
    for (int k = 0; k < numCourses; k++) {
      for (int i = 0; i < numCourses; i++) {
        for (int j = 0; j < numCourses; j++) {
          connected[i][j] = connected[i][j] || (connected[i][k] && connected[k][j]);
        }
      }
    }
    List<Boolean> result = new ArrayList<>();
    for (int[] query : queries) {
      result.add(connected[query[0]][query[1]]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/course-schedule-iv/submissions/1521678508/){:target="_blank"}

# 설명
1. $[0, numCourses - 1]$ 범위내 numCourses개 강의를 이용하여 prerequisites의 전제 조건을 만족하는 queries에 대한 결과를 각각 반환하는 문제이다.
- prerequisites[i] = [a<sub>i</sub>, b<sub>i</sub>] 로, b<sub>i</sub> 강의를 수강하기 위해서 a<sub>i</sub> 강의를 사전에 수강해야 한다는 의미를 나타낸다.
- queries[j] = [u<sub>j</sub>, v<sub>j</sub>] 로, u<sub>j</sub> 강의가 v<sub>j</sub> 강의의 사전 수강 강의인지 질의한다는 의미를 나타낸다.

2. 문제 풀이에 필요한 변수를 정의한다.
- connected는 연결된 강의 정보를 저장할 변수로, $numCourses \times numCourses$ 크기의 부울 배열로 초기화하고 아래를 수행한다.
  - prerequisites를 순차적으로 prerequisite에 넣어 connected[prerequisite[0]][prerequisite[1]] 위치에 true를 넣어 연결된 강의임을 체크해준다.
  - 0부터 numCourses 미만까지 k, i, j순으로 각 값을 증가시키며 반복하여, connected[i][j]의 위치에 connected[i][j]가 true인 연결된 강의거나 connected[i][k]와 connected[k][j]가 true인 i -> k -> j 순으로 강의를 들어야하는 경우에는 true를 아니면 false를 넣어준다.
- result는 queries의 각 결과를 저장할 변수로, ArrayList로 초기화하여 queries를 순차적으로 query에 넣어 connected[query[0]][query[1]] 값을 넣어준다.

3. queries의 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CourseScheduleIV.java){:target="_blank"}에서 확인 가능합니다.