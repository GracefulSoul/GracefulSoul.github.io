---
title: "Leetcode Java Range Sum of Sorted Subarray Sums"
excerpt: "Leetcode Range Sum of Sorted Subarray Sums Java"
last_modified_at: 2024-08-04T09:20:00
header:
  image: /assets/images/leetcode/range-sum-of-sorted-subarray-sums.png
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
[Link](https://leetcode.com/problems/range-sum-of-sorted-subarray-sums/){:target="_blank"}

# 코드
```java
class Solution {

  public int rangeSum(int[] nums, int n, int left, int right) {
    int mod = 1000000007;
    int result = 0;
    Queue<int[]> queue = new PriorityQueue<>(n, (p1, p2) -> p1[0] - p2[0]);
    for (int i = 0; i < n; i++) {
      queue.offer(new int[] { nums[i], i });
    }
    for (int i = 1; i <= right; i++) {
      int[] pair = queue.poll();
      if (i >= left) {
        result = (result + pair[0]) % mod;
      }
      if (pair[1] < n - 1) {
        pair[1]++;
        pair[0] = (pair[0] + nums[pair[1]]) % mod;
        queue.offer(pair);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/range-sum-of-sorted-subarray-sums/submissions/1343642436/){:target="_blank"}

# 설명
1. n 크기의 nums를 이용하여 모든 부분 배열의 합을 계산하여 오름차순으로 정렬하여 $n \times \frac{n + 1}{2}$의 새 배열로 만들 때, [left, right] 범위 내 값들의 합을 반환하는 문제이다.
- 단, 답이 매우 클 수 있으므로 모듈러 $10^9 + 7$를 적용한 결과를 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- mod는 모듈러 $10^9 + 7$를 적용하기 위한 변수로, $10^9 + 7$ 값으로 초기화한다.
- result는 결과를 저장할 변수로, 0으로 초기화한다.
- queue는 반복을 통해 부분 배열을 생성하기 위한 변수로, 오름차순으로 정렬해서 저장하기 위해 n 크기의 PriorityQueue로 초기화하고 nums의 각 값을 순차적으로 값과 위치를 배열로 넣어준다.

3. 1부터 right 미만까지 i를 증가시키며 아래를 수행한다.
- pair에 queue에서 값을 꺼내 넣어준다.
- i가 left 이상인 경우, result에 pair의 값을 더해 mod로 나눈 나머지 값을 넣어준다.
- pair[1]의 값이 $n - 1$인 범위 내인 경우, pair[1]인 위치 값을 증가시켜주고 pair[0]인 값의 위치에 pair[0]과 nums[pair[1]]의 값을 더해준 후 mod로 나눈 값을 넣어준다.
- queue에 pair[0]pair[1]

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RangeSumofSortedSubarraySums.java){:target="_blank"}에서 확인 가능합니다.