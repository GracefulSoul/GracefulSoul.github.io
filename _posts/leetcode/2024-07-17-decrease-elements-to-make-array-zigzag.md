---
title: "Leetcode Java Decrease Elements To Make Array Zigzag"
excerpt: "Leetcode Medium - 'Decrease Elements To Make Array Zigzag' 문제 Java 풀이"
last_modified_at: 2024-07-17T18:30:00
header:
  image: /assets/images/leetcode/decrease-elements-to-make-array-zigzag.png
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
[Link](https://leetcode.com/problems/decrease-elements-to-make-array-zigzag/){:target="_blank"}

# 코드
```java
class Solution {

  public int movesToMakeZigzag(int[] nums) {
    int[] result = new int[2];
    int length = nums.length;
    for (int i = 0, left = 0, right = 0; i < length; i++) {
      left = i > 0 ? nums[i - 1] : 1001;
      right = i + 1 < length ? nums[i + 1] : 1001;
      result[i % 2] += Math.max(0, nums[i] - Math.min(left, right) + 1);
    }
    return Math.min(result[0], result[1]);
  }

}
```

# 결과
[Link](https://leetcode.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another/submissions/1322757909/){:target="_blank"}

# 설명
1. nums를 아래의 조건을 만족하는 지그재그 형태로 값을 변경 할 때, 걸리는 최소 횟수를 구하는 문제이다.
- 모든 짝수 인덱스 값은 인접한 값들보다 크다, $A[0] > A[1] < A[2] > A[3] < A[4] > ...$를 만족한다.
- 혹은 모든 홀수 인덱스 값은 인접한 값들보다 크다, $A[0] < A[1] > A[2] < A[3] > A[4] < ...$를 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 지그재그 형태로 값을 넣어가며 값 변경 횟수 계산을 수행할 변수로, 2 크기의 정수 배열로 초기화한다.
- length는 nums의 길이를 저장한 변수이다.

3. 0부터 length 미만까지 i를 증가시키고, 지그재그 값을 저장할 left와 right는 0으로 초기화 하여 아래를 반복한다.
- left에 i가 0보다 크면 nums의 $i - 1$번째 값을 넣어주고, 아니면 값의 상한인 1001을 넣어준다.
- right에 $i + 1$이 length보다 작으면 nums의 $i + 1$번째 값을 넣어주고, 아니면 값의 상한인 1001을 넣어준다.
- result의 $\frac{i}{2}$ 몫의 해당하는 위치에 0과 nums[i]에 left와 right 중 작은 값을 뺀 후 1을 더한 값 중 큰 값을 넣어준다.

4. 위의 반복이 완료되면 result의 두 값 중 가장 작은 횟수를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/DecreaseElementsToMakeArrayZigzag.java){:target="_blank"}에서 확인 가능합니다.