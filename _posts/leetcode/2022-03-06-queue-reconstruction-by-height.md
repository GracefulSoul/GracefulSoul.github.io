---
title: "Leetcode Java Queue Reconstruction by Height"
excerpt: "Leetcode - 'Queue Reconstruction by Height' 문제 Java 풀이"
last_modified_at: 2022-03-06T17:00:00
header:
  image: /assets/images/leetcode/queue-reconstruction-by-height.png
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
[Link](https://leetcode.com/problems/queue-reconstruction-by-height/){:target="_blank"}

# 코드
```java
class Solution {

  public int[][] reconstructQueue(int[][] people) {
    Arrays.sort(people, (p1, p2) -> {
      int val = p2[0] - p1[0];
      if (val == 0) {
        val = p1[1] - p2[1];
      }
      return val;
    });
    List<int[]> result = new ArrayList<>();
    for (int[] p : people) {
      result.add(p[1], p);
    }
    return result.toArray(new int[0][]);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/654385559/){:target="_blank"}

# 설명
1. 주어진 2차원 정수 배열인 people을 이용하여 아래의 조건을 활용하여 큐에 정렬하는 문제이다.
- people[i] = [h<sub>i</sub>, k<sub>i</sub>]이며, h는 키를 k는 자신 앞에 존재하는 인원들 중 자신보다 키가 큰 인원의 수를 의미한다.
- queue[j] = [h<sub>j</sub>, k<sub>j</sub>]이며, people이 j번째 큐에 존재하는 값을 의미한다.

2. 주어진 조건에 맞게 정렬하기 위해 임의 두 값을 p1과 p2라고 정의하고 people을 정렬한다.
- val에 p2의 첫 번째 값과 p1의 첫 번째 값의 차이를 넣어준다.
- val이 0인 경우 동일한 키를 의미하므로, val에 p1의 두 번째 값과 p2의 두 번째 값을 뺀 값인 자신의 앞에 키가 큰 인원의 수의 차이를 넣어준다.
- val이 반환된 값의 크기로 오름차순 정렬을 수행한다.

3. 정렬된 값들을 저장할 result를 ArrayList로 초기화하고, 정렬된 people을 result의 p[1] 값 위치에 p를 넣어준다.

4. 반복이 완료되면 reuslt를 2차원 정수 배열로 변경하여 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/QueueReconstructionByHeight.java){:target="_blank"}에서 확인 가능합니다.