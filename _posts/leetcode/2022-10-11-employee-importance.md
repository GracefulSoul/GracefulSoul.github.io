---
title: "Leetcode Java Employee Importance"
excerpt: "Leetcode Employee Importance Java"
last_modified_at: 2022-10-11T19:50:00
header:
  image: /assets/images/leetcode/employee-importance.png
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
[Link](https://leetcode.com/problems/employee-importance){:target="_blank"}

# 코드
```java
/*
// Definition for Employee.
class Employee {
    public int id;
    public int importance;
    public List<Integer> subordinates;
};
*/

class Solution {

  public int getImportance(List<Employee> employees, int id) {
    Map<Integer, Employee> map = new HashMap<>();
    for (Employee employee : employees) {
      map.put(employee.id, employee);
    }
    Queue<Integer> queue = new LinkedList<>();
    queue.add(id);
    int importance = 0;
    while (!queue.isEmpty()) {
      int size = queue.size();
      while (size-- > 0) {
        Employee employee = map.get(queue.poll());
        importance += employee.importance;
        queue.addAll(employee.subordinates);
      }
    }
    return importance;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/820058754/){:target="_blank"}

# 설명
1. employees에서 아이디가 id에 해당하는 직원의 모든 부하 직원의 중요도 합을 반환하는 문제이다.

2. map은 모든 직원 정보를 저장할 변수로, HashMap으로 초기화하고 employees의 모든 객체를 id가 key인 value로 map에 넣어준다.

3. queue는 모든 직원의 id 값을 넣어 BFS 방식으로 탐색하기 위한 변수로, LinkedList로 초기화하고 id를 넣어준다.

4. 아이디가 id인 직원의 모든 부하 직원의 중요도 합을 저장할 importance를 0으로 초기화한다.

5. queue가 비어있지 않을 때까지 아래를 반복한다.
- size에 queue의 크기를 넣어준다.
- size가 0 초과일 때 까지 아래를 수행하고 size를 감소시킨다.
  - employee에 queue에서 꺼낸 아이디를 이용하여 map에서 꺼낸 직원 정보를 저장한다.
  - importance에 employee의 importance 값을 더해준다.
  - queue에 employee의 부하 직원 아이디 값인 subordinates를 모두 넣어주고 반복을 계속 수행한다.

6. 반복이 완료되면 계산된 중요도인 importance를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/EmployeeImportance.java){:target="_blank"}에서 확인 가능합니다.