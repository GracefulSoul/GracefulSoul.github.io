---
title: "Leetcode Java Maximum Subsequence Score"
excerpt: "Leetcode Maximum Subsequence Score Java"
last_modified_at: 2023-05-24T20:20:00
header:
  image: /assets/images/leetcode/maximum-subsequence-score.png
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
[Link](https://leetcode.com/problems/maximum-subsequence-score){:target="_blank"}

# 코드
```java
class Solution {

  public long maxScore(int[] nums1, int[] nums2, int k) {
    int length = nums1.length;
    int[][] pairs = new int[length][2];
    for (int i = 0; i < length; i++) {
      pairs[i] = new int[] { nums1[i], nums2[i] };
    }
    Arrays.sort(pairs, (a, b) -> b[1] - a[1]);
    Queue<Integer> queue = new PriorityQueue<>(k, (a, b) -> a - b);
    long result = 0;
    long sum = 0;
    for (int[] pair : pairs) {
      queue.offer(pair[0]);
      sum += pair[0];
      if (queue.size() > k) {
        sum -= queue.poll();
      }
      if (queue.size() == k) {
        result = Math.max(result, sum * pair[1]);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/maximum-subsequence-score/submissions/956394327/){:target="_blank"}

# 설명
1. num1의 k개 값과 동일한 위치의 nums2의 k개 값 중 작은 값과의 곱한 값이 가장 큰 결과를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums1의 길이를 저장할 변수이다.
- pairs는 nums1과 nums2의 공통된 위치 값을 저장할 변수로, $length \times 2$ 크기로 초기화하고 두 배열을 반복하여 pairs에 동일한 위치 값끼리 넣어준 후 nums2 값 기준으로 내림차순 정렬한다.
- queue는 k개의 값을 오름차순 정렬된 값을 저장할 변수로, PriorityQueue를 k 초기 크기로 초기화한다.
- result는 결과를 넣을 변수로, 0으로 초기화한다.
- sum은 세 값의 합을 저장할 변수로, 0으로 초기화한다.

3. pairs의 모든 값들을 pair에 넣어 아래를 수행한다.
- queue에 pair의 첫 값을 넣고, 해당 값을 sum에 더해준다.
- queue의 크기가 k 초과인 경우 queue에서 가장 작은 값을 꺼내 제거한다.
- queue의 크기가 k와 동일한 경우, result에 result와 $sum \times pair[1]$의 결과 중 큰 값을 넣어준다.

4. 반복이 완료되면 가장 큰 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumSubsequenceScore.java){:target="_blank"}에서 확인 가능합니다.