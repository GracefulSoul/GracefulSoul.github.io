---
title: "Leetcode Java Maximize Distance to Closest Person"
excerpt: "Leetcode Maximize Distance to Closest Person Java"
last_modified_at: 2023-02-22T19:50:00
header:
  image: /assets/images/leetcode/maximize-distance-to-closest-person.png
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
[Link](https://leetcode.com/problems/maximize-distance-to-closest-person){:target="_blank"}

# 코드
```java
class Solution {

  public int maxDistToClosest(int[] seats) {
    int length = seats.length;
    int result = 0;
    int left = -1;
    for (int right = 0; right < length; right++) {
      if (seats[right] == 1) {
        if (left == -1) {
          result = right;
        } else {
          result = Math.max(result, (right - left) / 2);
        }
        left = right;
      }
    }
    return seats[length - 1] == 1 ? result : Math.max(result, length - 1 - left);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximize-distance-to-closest-person/submissions/902853390/){:target="_blank"}

# 설명
1. 좌석에 사람이 있으면 1, 없으면 0으로 표시된 seats에서 좌우 사람들 간 거리가 가장 먼 자리의 위치를 찾는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 seats의 길이를 저장한 변수이다.
- result는 좌우 사람들 간 거리가 가장 먼 거리의 위치를 저장할 변수로, 0으로 초기화한다.
- left는 좌측 사람과의 거리를 저장하기 위한 변수로, 최소 위치보다 작은 -1로 초기화한다.

3. right를 0부터 length 미만까지 right를 증가시키며 아래를 반복한다.
- seats의 right번째 위치에 사람이 존재하는 1인 경우, 아래를 수행한다.
  - left가 -1인 초기 위치인 경우, result에 right를 넣어준다.
  - 위의 경우가 아니라면 result에 result와 $\frac{right - left}{2}$의 중간 위치를 넣어준다.
  - left에 right를 넣어 마지막 사람 위치를 저장한다.

4. 마지막으로 seats의 마지막 위치인 $length - 1$ 뻔째 값이 1이면 result를, 0인 빈 자리이면 left와의 거리 차이와 right 중 큰 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximizeDistanceToClosestPerson.java){:target="_blank"}에서 확인 가능합니다.