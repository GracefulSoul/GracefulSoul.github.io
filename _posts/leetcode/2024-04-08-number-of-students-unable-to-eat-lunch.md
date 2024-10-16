---
title: "Leetcode Java Number of Students Unable to Eat Lunch"
excerpt: "Leetcode Number of Students Unable to Eat Lunch Java"
last_modified_at: 2024-04-08T19:20:00
header:
  image: /assets/images/leetcode/number-of-students-unable-to-eat-lunch.png
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
[Link](https://leetcode.com/problems/number-of-students-unable-to-eat-lunch/){:target="_blank"}

# 코드
```java
class Solution {

  public int countStudents(int[] students, int[] sandwiches) {
    int[] count = { 0, 0 };
    int length = students.length;
    for (int student : students) {
      count[student]++;
    }
    for (int k = 0; 0 < length && 0 < count[sandwiches[k]]; k++, length--) {
      count[sandwiches[k]]--;
    }
    return length;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/number-of-students-unable-to-eat-lunch/submissions/1226602851/){:target="_blank"}

# 설명
1. 학생 별 좋아하는 샌드위치 번호를 담은 students를 이용하여 순서대로 sandwiches의 샌드위치를 가져갈 때, 먹을 수 없는 학생의 수를 구하는 문제이다.
- 학생이 선호하는 샌드위치가 아닌 경우, students의 맨 뒤로 이동하여 다시 대기한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 유형 별 샌드위치 갯수를 저장할 변수로, 2차원 배열로 초기화하여 샌드위치의 종류 별 갯수를 넣어준다.
- length는 students의 길이인 학생의 수를 저장한 변수이다.

3. k가 0부터 length가 0 초과이면서 count[sandwiches[k]]의 값이 0보다 클 때까지 k를 증가시키고 length를 감소시키며, count[sandwiches[k]]의 값을 감소시킨다.

4. 반복이 종료되면 샌드위치를 가져가지 못한 학생의 수인 length를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NumberOfStudentsUnableToEatLunch.java){:target="_blank"}에서 확인 가능합니다.