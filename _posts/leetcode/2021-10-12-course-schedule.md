---
title: "Leetcode Java Course Schedule"
excerpt: "Leetcode Course Schedule Java 풀이"
last_modified_at: 2021-10-12T12:00:00
header:
  image: /assets/images/leetcode/course-schedule.png
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
[Link](https://leetcode.com/problems/course-schedule/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean canFinish(int numCourses, int[][] prerequisites) {
    List<Integer>[] graph = new List[numCourses];
    int[] courses = new int[numCourses];
    for (int i = 0; i < numCourses; i++) {
      graph[i] = new ArrayList<>();
    }
    for (int[] req : prerequisites) {
      graph[req[1]].add(req[0]);
      courses[req[0]]++;
    }
    ArrayList<Integer> result = new ArrayList<>();
    for (int i = 0; i < numCourses; i++) {
      if (courses[i] == 0) {
        result.add(i);
      }
    }
    for (int i = 0; i < result.size(); i++) {
      for (int course : graph[result.get(i)]) {
        if (--courses[course] == 0) {
          result.add(course);
        }
      }
    }
    return result.size() == numCourses;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/569784227/){:target="_blank"}

# 설명
1. 주어진 정수 numCourses는 수강해야 하는 총 과목 수로, 주어진 2차원 배열 prerequisites를 이용하여 numCourses 만큼의 과목을 수료할 수 있는지 검증하는 문제이다.
- prerequisites은 각 과목 정보를 [과목 번호, 선행 과목 번호]로 담고 있으며, 이는 해당 과목을 수료하기 위해선 선행 과목을 수료해야 함을 나타낸다.

2. 문제 풀이에 필요한 변수를 정의한다.
- graph는 선행 과목을 수료했을 경우 수강 가능한 과목 번호를 저장할 컬렉션의 배열이다.
- courses는 과목 존재 여부에 대한 정보를 담은 배열이다.

3. 0부터 numCourses 전까지 반복하여 graph에 ArrayList를 다 넣어준다.

4. 수료 가능한 과목 번호를 담을 result 컬렉션을 정의하고, 0부터 numCourses까지 반복하여 과목 정보가 없을 경우 과목 번호를 넣어준다.

5. result 배열을 순회하여 graph[result.get(i)]에 존재하는 값들을 반복하여 courses[course]에 저장된 과목 정보를 감소시키며 result에 course 번호를 넣어준다.
- graph[result.get(i)] 저장된 값들은 result의 i번째 과목을 수료했을 경우, 수료 가능한 과목의 코드들이다.
- 위의 해당 값을 반복하여 courses의 값을 감소시키고, result에 해당 과목을 넣어 수강 과목 목록에 추가시키는 것이다.

6. 수료 가능한 과목의 갯수인 result의 크기와 numCourses가 동일한지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CourseSchedule.java){:target="_blank"}에서 확인 가능합니다.