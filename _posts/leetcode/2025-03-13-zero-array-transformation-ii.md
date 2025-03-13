---
title: "Leetcode Java Zero Array Transformation II"
excerpt: "Leetcode - 'Zero Array Transformation II' 문제 Java 풀이"
last_modified_at: 2025-03-13T18:30:00
header:
  image: /assets/images/leetcode/zero-array-transformation-ii.png
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
[Link](https://leetcode.com/problems/zero-array-transformation-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int minZeroArray(int[] nums, int[][] queries) {
    int length = nums.length;
    int sum = 0;
    int result = 0;
    int[] counts = new int[length + 1];
    for (int i = 0; i < length; i++) {
      while (sum + counts[i] < nums[i]) {
        if (result == queries.length) {
          return -1;
        } else {
          int l = queries[result][0];
          int r = queries[result][1];
          int val = queries[result][2];
          result++;
          if (i <= r) {
            counts[Math.max(l, i)] += val;
            counts[r + 1] -= val;
          }
        }
      }
      sum += counts[i];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/zero-array-transformation-ii/submissions/1572325445/){:target="_blank"}

# 설명
1. 정수 배열로 이루어진 nums를 이용하여 아래 규칙대로 적용하여 모든 값이 0이 되기 위한 queries의 위치를 찾는 문제이다.
- queries[i] = [l<sub>i</sub>, r<sub>i</sub>, val<sub>i</sub>]로,  [l<sub>i</sub>, r<sub>i</sub>] 범위 내 값들을 val<sub>i</sub>만큼 감소시킨다는 의미이다.
- 각 감소되는 위치 별 값은 0 미만으로 내려가지 않는다.
- 해당 위치가 존재하지 않는 경우, -1을 주어진 문제의 결과로 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- sum은 위치 별 감소될 값을 합쳐 저장할 변수로, 0으로 초기화한다.
- result는 nums의 모든 값을 0으로 되기까지 적용한 queries의 위치를 계산할 변수로, 0으로 초기화한다.
- counts는 각 위치 별 차감되는 갯수를 누계하기 위한 변수로, $length - 1$크기의 정수 배열로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키면서 아래를 반복한다.
- $sum + counts[i]$의값이 nums[i] 미만인 차감 가능할 때 까지 아래를 반복한다.
  - result가 queries의 길이와 동일한 모든 쿼리 수행이 완료된 경우, 모든 위치의 값이 0으로 될 수 없으므로 -1을 주어진 문제의 결과로 반환한다.
  - 위의 경우가 아니라면 l, r, val에 queries[result]의 값들을 순차적으로 넣고 result를 증가시킨 후, i가 r보다 작다면 counts 내 l과 i 중 큰 값에 해당하는 위치에 val을 더해주고, counts[$r + 1$]의 값을 val만큼 감소시켜준다.
- sum에 counts[i]의 값을 더해 감소되는 값을 증가시켜준다.

4. 반복이 완료되면 적용된 queries의 갯수인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ZeroArrayTransformationII.java){:target="_blank"}에서 확인 가능합니다.