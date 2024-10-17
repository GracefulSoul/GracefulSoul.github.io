---
title: "Leetcode Java Boats to Save People"
excerpt: "Leetcode - 'Boats to Save People' 문제 Java 풀이"
last_modified_at: 2023-03-23T19:10:00
header:
  image: /assets/images/leetcode/boats-to-save-people.png
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
[Link](https://leetcode.com/problems/boats-to-save-people){:target="_blank"}

# 코드
```java
class Solution {

  public int numRescueBoats(int[] people, int limit) {
    Arrays.sort(people);
    int i = 0;
    int j = people.length - 1;
    int result = 0;
    while (i <= j) {
      result++;
      if (people[i] + people[j--] <= limit) {
        i++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/boats-to-save-people/submissions/920692308/){:target="_blank"}

# 설명
1. 사람의 몸무게가 담긴 people을 이용하여 limit 이하인 사람들의 그룹을 만드는 문제이다.

2. people을 오름차순으로 정렬하여 작은 몸무게인 사람들을 앞으로 모아준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- i와 j는 몸무게 조합을 생성하기 위한 변수로, people의 처음 위치와 마지막 위치를 넣어준다.
- result는 그룹의 수를 저장하기 위한 변수로, 0으로 초기화한다.

4. i가 j 이하일 때 까지 아래를 반복한다.
- 하나의 군집을 생성할 수 있으므로 result를 증가시킨다.
- i번쨰 사람과 j번째 사람이 limit 이하인 경우, i를 증가시켜 범위를 좁혀주고 j를 감소시킨다.

5. 반복이 완료되면 그룹의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BoatsToSavePeople.java){:target="_blank"}에서 확인 가능합니다.