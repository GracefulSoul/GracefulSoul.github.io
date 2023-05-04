---
title: "Leetcode Java Partition Array into Disjoint Intervals"
excerpt: "Leetcode Partition Array into Disjoint Intervals Java"
last_modified_at: 2023-05-04T19:55:00
header:
  image: /assets/images/leetcode/partition-array-into-disjoint-intervals.png
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
[Link](https://leetcode.com/problems/partition-array-into-disjoint-intervals){:target="_blank"}

# 코드
```java
class Solution {

  public int partitionDisjoint(int[] nums) {
    int index = 0;
    int prev = nums[0];
    int max = prev;
    for (int i = 1; i < nums.length; i++) {
      if (prev > nums[i]) {
        prev = max;
        index = i;
      } else {
        max = Math.max(max, nums[i]);
      }
    }
    return index + 1;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/partition-array-into-disjoint-intervals/submissions/944307549/){:target="_blank"}

# 설명
1. 정수 배열인 nums를 이용하여 아래의 규칙을 만족하는 부분 배열로 분리하였을 때, 왼쪽 배열의 길이를 반환하는 문제이다.
- 두 배열은 한 지점에서 갈라진 두 배열로, 빈 배열이 없다.
- 왼쪽 배열의 모든 값은 오른쪽 배열의 모든 값들보다 작거나 같다.
- 왼쪽 배열은 가능한 가장 작은 크기를 가진다.

2. 문제 풀이에 필요한 변수를 정의한다.
- index는 좌측 배열의 마지막 위치를 저장하기 위한 변수로, 0으로 초기화한다.
- prev는 이전 위치까지 max는 현재까지 큰 값을 저장하기 위한 변수로, 둘 다 nums의 첫 값으로 초기화한다.

3. 1부터 nums의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- prev가 현재 위치 값인 nums의 i번째 값보다 큰 경우, prev에 가장 큰 값인 max를 넣고 index에 i를 넣어준다.
- 위가 아니라면 max에 현재까지 가장 큰 값을 넣어준다.

4. 반복이 완료되면 $index + 1$인 좌측 배열의 길이를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PartitionArrayIntoDisjointIntervals.java){:target="_blank"}에서 확인 가능합니다.