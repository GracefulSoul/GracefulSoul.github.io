---
title: "Leetcode Java Next Greater Element II"
excerpt: "Leetcode - 'Next Greater Element II' 문제 Java 풀이"
last_modified_at: 2022-05-23T13:00:00
header:
  image: /assets/images/leetcode/next-greater-element-ii.png
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
[Link](https://leetcode.com/problems/next-greater-element-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] nextGreaterElements(int[] nums) {
    int length = nums.length;
    int[] result = new int[length];
    Deque<int[]> deque = new ArrayDeque<>();
    Arrays.fill(result, -1);
    for (int idx = 0; idx < length * 2; idx++) {
      while (!deque.isEmpty() && deque.peek()[0] < nums[idx % length]) {
        result[deque.removeFirst()[1]] = nums[idx % length];
      }
      if (idx < length) {
        deque.addFirst(new int[] { nums[idx], idx });
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/705182139/){:target="_blank"}

# 설명
1. 원형으로 순환되는 정수 배열인 nums의 각 요소의 우측에서 가장 가까우면서 현재 값보다 큰 값을 검색하고, 검색한 값들을 동일한 위치의 정수 배열로 만들어 반환하는 문제이다.
- 단 현재 위치의 값이 나머지 값보다 커서 해당 값보다 큰 값이 존재하지 않는 경우, -1을 넣어준다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장할 변수이다.
- result는 결과를 저장할 변수로, length 크기의 정수 배열로 초기화하고 모든 위치에 존재하지 않을 경우에 대한 값인 -1을 넣어준다.
- deque는 nums의 값을 위치 별 저장해서 순서 별 꺼내 사용하기 위한 변수로, ArrayDeque로 초기화한다.

3. 0부터 $length \times 2$ 미만까지 idx를 증가시키며 아래를 반복한다.
- deque가 비어있지 않고, deque의 첫 배열의 nums 내 숫자가 nums의 idx % length 번째 값보다 작은 경우 해당 위치의 값보다 크므로 아래를 수행한다.
  - deque에서 첫 번째 배열을 꺼내 위치 값에 해당하는 result의 위치에 idx % length 번째 값을 넣어준다.
- idx가 length보다 작을 경우, deque의 첫 값에 nums의 idx번째 값과 idx를 배열로 만들어 넣어준다.

4. 반복이 완료되면 nums의 각 요소 별 값보다 가장 가까운 우측의 큰 값을 넣은 result를 주어진 문제의 결과로 반환한다.

# 해설
반복의 상한이 $length \times 2$ 이고, nums의 idx % length 번째 값을 가져오는 이유는 원형으로 순환된다는 전제이기 때문에 최소 횟수의 순환으로 원하는 결과를 탐색하기 위한 아이디어이다.
- 예를 들어 nums의 배열의 크기가 2인 경우, 위를 통해 nums[0] -> nums[1] -> nums[0] -> nums[1] 순서로 수행하면서 nums[1]보다 우측에 있는 nums[0]의 크기와 비교한 결과를 사용할 수 있다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NextGreaterElementII.java){:target="_blank"}에서 확인 가능합니다.