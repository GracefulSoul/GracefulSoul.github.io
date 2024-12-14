---
title: "Leetcode Java Continuous Subarrays"
excerpt: "Leetcode - 'Continuous Subarrays' 문제 Java 풀이"
last_modified_at: 2024-12-14T13:00:00
header:
  image: /assets/images/leetcode/continuous-subarrays.png
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
[Link](https://leetcode.com/problems/continuous-subarrays/){:target="_blank"}

# 코드
```java
class Solution {

  public long continuousSubarrays(int[] nums) {
    long result = 0;
    Deque<Integer> ascending = new LinkedList<>();
    Deque<Integer> descending = new LinkedList<>();
    for (int i = 0, j = -1; i < nums.length; i++) {
      while (!ascending.isEmpty() && ascending.peekLast() > nums[i]) {
        ascending.pollLast();
      }
      ascending.add(nums[i]);
      while (!descending.isEmpty() && descending.peekLast() < nums[i]) {
        descending.pollLast();
      }
      descending.add(nums[i]);
      while (descending.peekFirst() - ascending.peekFirst() > 2) {
        j++;
        if (ascending.peekFirst() == nums[j]) {
          ascending.pollFirst();
        }
        if (descending.peekFirst() == nums[j]) {
          descending.pollFirst();
        }
      }
      result += i - j;
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/continuous-subarrays/submissions/1478324244/){:target="_blank"}

# 설명
1. nums에서 아래 조건을 만족하는 연속된 부분 배열의 갯수를 계산하는 문제이다.
- i <= i1, i2 <= j일 때, $0 <= |nums[i1] - nums[i2]| <= 2$를 만족한다.
- 자기 자신은 부분 배열에 속하지 않는다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 부분 배열의 갯수를 계산할 변수로, 0으로 초기화한다.
- ascending과 descending은 오름차순, 내림차순으로 값들을 저장하기 위한 변수로, LinkedList로 초기화한다.

3. 0부터 nums의 길이 미만까지 i를 증가시키고, j는 -1로 초기화 하여 아래를 반복한다.
- ascending이 비어있지 않고 ascending의 마지막 값이 nums[i]보다 큰 경우, ascending에서 마지막 값을 꺼내준 후 마지막으로 nums[i]를 넣어준다.
- descending이 비어있지 않고 descending의 마지막 값이 nums[i]보다 큰 경우, descending에서 마지막 값을 꺼내준 후 마지막으로 nums[i]를 넣어준다.
- descending의 첫 값과 ascending의 첫 값의 차이가 2보다 큰 조건이 만족하지 않는 경우까지 아래를 반복한다.
  - j를 증가시켜 위치를 이동한다.
  - ascending의 첫 값이 nums[j]의 값과 동일하면 해당 값을 제거한다.
  - descending의 첫 값이 nums[j]의 값과 동일하면 해당 값을 제거한다.
- result에 [i, j] 범위 내 부분 배열의 갯수인 $i - j$를 더해준다.

4. 반복이 완료되면 갯수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/ContinuousSubarrays.java){:target="_blank"}에서 확인 가능합니다.