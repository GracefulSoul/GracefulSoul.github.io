---
title: "Leetcode Java Magnetic Force Between Two Balls"
excerpt: "Leetcode Magnetic Force Between Two Balls Java"
last_modified_at: 2024-06-20T21:10:00
header:
  image: /assets/images/leetcode/magnetic-force-between-two-balls.png
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
[Link](https://leetcode.com/problems/magnetic-force-between-two-balls/){:target="_blank"}

# 코드
```java
class Solution {

  public int maxDistance(int[] position, int m) {
    Arrays.sort(position);
    int left = 0;
    int right = position[position.length - 1];
    int result = 0;
    while (left < right) {
      int mid = left + (right - left) / 2;
      if (this.isPossible(position, m, mid)) {
        result = mid;
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return result;
  }

  private boolean isPossible(int[] positions, int m, int max) {
    int count = 1;
    int prev = positions[0];
    for (int i = 1; i < positions.length; i++) {
      if (positions[i] - prev >= max) {
        prev = positions[i];
        count++;
      }
    }
    return count >= m;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/magnetic-force-between-two-balls/submissions/1294584201/){:target="_blank"}

# 설명
1. n개의 바구니에 m개 공을 넣을 떄, 각 공 사이의 최소 거리가 최댓 값보다 크거나 같도록 위치할 때 각 공 사이의 최소 거리를 반환하는 문제이다.

2. position을 오름차순 정렬해준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- left와 right는 탐색에 필요한 위치 변수로, 0과 position의 마지막 값으로 초기화해준다.
- result는 각 공 사이의 최소 거리를 저장할 변수로, 0으로 초기화한다.

4. left가 right 미만일 때 까지 아래를 반복한다.
- mid는 중앙값을 저장할 변수로, $left + \frac{right - left}{2}$를 넣어준다.
- 5번에서 정의한 isPossible(int[] positions, int m, int max) 메서드의 max 자리에 mid를 넣어 수행한 결과가 만족하는지 여부에 따라 아래를 수행한다.
  - 위의 결과가 true이면 조건을 만족하도록 공을 바구니에 분배 가능하므로, result에 mid를 넣고 left에 $mid + 1$을 넣어 하단 범위를 높혀준다.
  - 위의 결과가 false이면 조건을 만족하도록 공을 바구니에 분배할 수 없으므로, right에 mid를 넣어 상단 범위를 낮춰준다.

5. 주어진 조건에 따라 공을 바구니에 분배할 수 있는지 검증하기 위한 isPossible(int[] positions, int m, int max) 메서드를 정의한다.
- 검증에 필요한 변수를 정의한다.
  - count는 바구니에 공을 넣은 갯수를 계산할 변수로, 첫 바구니는 반드시 포함되므로 1로 초기화한다.
  - prev는 이전 바구니의 값을 저장할 변수로, positions[0]의 값으로 초기화한다.
- 1부터 positions의 길이 미만까지 i를 증가시키며 아래를 수행한다.
  - $positions[i] - prev >= max$이면 조건을 만족하므로 prev에 positions[i] 값을 넣고 count를 증가시켜준다.
- 반복이 완료되면 count가 m 이상인 바구니에 공을 모두 분배 가능한지 검증한 결과를 반환한다.

6. 모든 수행이 완료되면 최소 거리가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MagneticForceBetweenTwoBalls.java){:target="_blank"}에서 확인 가능합니다.