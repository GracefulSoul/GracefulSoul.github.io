---
title: "Leetcode Java Car Pooling"
excerpt: "Leetcode Medium - 'Car Pooling' 문제 Java 풀이"
last_modified_at: 2024-04-28T10:10:00
header:
  image: /assets/images/leetcode/car-pooling.png
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
[Link](https://leetcode.com/problems/car-pooling/){:target="_blank"}

# 코드
```java
class Solution {

  public boolean carPooling(int[][] trips, int capacity) {
    int[] count = new int[1001];
    for (int t[] : trips) {
      count[t[1]] += t[0];
      count[t[2]] -= t[0];
    }
    for (int i = 0; capacity >= 0 && i < count.length; i++) {
      capacity -= count[i];
    }
    return capacity >= 0;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/car-pooling/submissions/1243693979/){:target="_blank"}

# 설명
1. capacity 좌석이 비어있는 차에서 [승객, 출발지, 도착지]가 저장된 trips를 이용하여 모든 승객들이 도착지에 도달할 수 있는지를 검증하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 승객의 수를 저장할 변수로, 최대 가능한 값의 상한인 1000보다 1 큰 크기의 정수 배열로 초기화하고 trips를 반복하여 출발지와 도착지의 승객들을 가감해준다.

3. 0부터 count의 길이 미만까지 i를 증가시키며, capacity가 0 이상일 때 까지 아래를 반복하여 capacity의 값에 count[i] 값을 차감해준다.

4. 반복이 완료되면 capacity가 0 이상인 좌석이 여유있는지 여부를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CarPooling.java){:target="_blank"}에서 확인 가능합니다.