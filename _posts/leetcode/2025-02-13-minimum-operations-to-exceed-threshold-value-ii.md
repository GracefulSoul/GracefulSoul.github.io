---
title: "Leetcode Java Minimum Operations to Exceed Threshold Value II"
excerpt: "Leetcode - 'Minimum Operations to Exceed Threshold Value II' 문제 Java 풀이"
last_modified_at: 2025-02-13T18:20:00
header:
  image: /assets/images/leetcode/minimum-operations-to-exceed-threshold-value-ii.png
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
[Link](https://leetcode.com/problems/minimum-operations-to-exceed-threshold-value-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int minOperations(int[] nums, int k) {
    Queue<Integer> queue = new PriorityQueue<>();
    for (int num : nums) {
      if (num < k) {
        queue.add(num);
      }
    }
    int result = 0;
    while (!queue.isEmpty()) {
      int x = queue.poll();
      result++;
      if (queue.isEmpty()) {
        break;
      } else {
        int y = queue.poll();
        long value = (2L * x) + y;
        if (value < k) {
          queue.add((int) value);
        }
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-operations-to-exceed-threshold-value-ii/submissions/1541543065/){:target="_blank"}

# 설명
1. nums의 모든 값이 k 이상이 되도록 하기 위한 아래 수행을 반복할 때, 최소 작업의 횟수를 구하는 문제이다.
- nums의 가장 작은 값을 제거하고 x와 y에 넣은 후, 배열의 임의 위치에 $min(x, y) \times 2 + max(x, y)$를 추가한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- queue는 nums의 k 이하인 값을 저장할 변수로, 오름차순 값을 정렬하여 저장하기 위해 PriorityQueue로 초기화하고 nums를 반복하여 k 미만인 값을 넣어준다.
- result는 최소 반복 횟수를 계산하기 위한 변수로, 0으로 초기화한다.

3. queue가 비어있지 않을 때 까지 아래를 반복한다.
- x는 가장 작은 값을 저장할 변수로, queue의 첫 값을 넣어준다.
- result인 꺼낸 횟수를 증가시켜준다.
- queue가 비어있으면 반복을 중지시키고, 비어있지 않으면 아래를 수행한다.
  - y에 queue의 x 이후 가장 작은 값을 넣어준다.
  - value는 조건인 $(2L \times x) + y$를 수행한 결과를 넣어준다.
  - value가 k 미만인 경우, queue에 value를 넣어 다시 반복을 수행할 대상으로 추가한다.

4. 반복이 완료되면 최소 작업의 횟수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumOperationsToExceedThresholdValueII.java){:target="_blank"}에서 확인 가능합니다.