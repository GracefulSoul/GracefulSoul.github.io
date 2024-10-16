---
title: "Leetcode Java Course Schedule II"
excerpt: "Leetcode Course Schedule II Java 풀이"
last_modified_at: 2021-10-15T12:00:00
header:
  image: /assets/images/leetcode/course-schedule-ii.png
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
[Link](https://leetcode.com/problems/course-schedule-ii/){:target="_blank"}

# 코드
```java
class Solution {
  
  public int[] findOrder(int numCourses, int[][] prerequisites) {
    List<Integer>[] graph = new ArrayList[numCourses];
    int[] courses = new int[numCourses];
    for (int i = 0; i < numCourses; i++) {
      graph[i] = new ArrayList<>();
    }
    for (int[] req : prerequisites) {
      courses[req[0]]++;
      graph[req[1]].add(req[0]);
    }
    int index = 0;
    int[] result = new int[numCourses];
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < numCourses; i++) {
      if (courses[i] == 0) {
        queue.add(i);
        result[index++] = i;
      }
    }
    while (!queue.isEmpty()) {
      int cur = queue.poll();
      for (int course : graph[cur]) {
        if (--courses[course] == 0) {
          queue.add(course);
          result[index++] = course;
        }
      }
    }
    return index == numCourses ? result : new int[0];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/571367795/){:target="_blank"}

# 설명
1. 지난번 [Course Schedule](../course-schedule)과 유사하지만, 주어진 정수 numCourses는 수강해야 하는 총 과목 수로, 주어진 2차원 배열 prerequisites를 이용하여 수료 가능한 과목 번호를 찾는 문제이다.
- prerequisites은 각 과목 정보를 [과목 번호, 선행 과목 번호]로 담고 있으며, 이는 해당 과목을 수료하기 위해선 선행 과목을 수료해야 함을 나타낸다.

2. 문제 풀이에 필요한 변수를 정의한다.
- graph는 선행 과목을 수료했을 경우 수강 가능한 과목 번호를 저장할 컬렉션의 배열이다.
- courses는 과목 존재 여부에 대한 정보를 담은 배열이다.

3. 0부터 numCourses 전까지 반복하여 graph에 ArrayList를 다 넣어준다.

4. 문제 풀이에 필요한 추가 변수를 정의한다.
- index는 아래의 result 배열에 과목 번호를 담을 위치를 지정한다.
- result는 수료 가능한 과목 번호를 담을 배열로, numCourses 크기로 정의한다.
- queue는 수료 가능한 과목 번호를 임시로 담을 큐이다.

5. courses 배열을 처음부터 끝까지 반복하여 courses[i]의 값이 0일 경우만 아래를 수행한다.
- queue와 result[index]에 i를 넣어주고 index는 증가시킨다.

6. queue의 값들을 모두 사용할 때 까지 반복하여 아래를 수행한다.
- queue에 저장된 값을 꺼내와 graph의 해당 값인 수료 가능한 과목 번호를 각 course로 정의하여 아래를 반복한다.
- courses[course]의 값을 1 감소시킨 결과가 0인 경우 해당 course 수행 이후 다음 수료 과목을 탐색해야 하므로, queue에 다시 course 값을 넣어준다.
- result의 index번째 값에 course 값을 넣어주고, index를 증가시킨다.

7. index와 numCourses의 값들이 동일한지를 검증하여 결과를 반환한다.
- index와 numCourses의 값들이 동일하면, 수료 가능한 과목들을 모두 채운 result를 주어진 문제의 결과로 반환한다.
- index와 numCourses의 값들이 동일하지 않으면, 수료 가능한 과목들을 모두 채우지 못하므로 새로운 배열을 만들어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CourseScheduleII.java){:target="_blank"}에서 확인 가능합니다.