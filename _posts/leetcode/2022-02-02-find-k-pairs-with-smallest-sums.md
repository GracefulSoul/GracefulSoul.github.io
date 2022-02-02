---
title: "Leetcode Java Find K Pairs with Smallest Sums"
excerpt: "Leetcode Find K Pairs with Smallest Sums Java 풀이"
last_modified_at: 2022-02-02T17:00:00
header:
  image: /assets/images/leetcode/find-k-pairs-with-smallest-sums.png
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
[Link](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/){:target="_blank"}

# 코드
```java
class Solution {

  public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
    List<List<Integer>> result = new ArrayList<>();
    Queue<int[]> queue = new PriorityQueue<>((a, b) -> (a[0] + a[1] - b[0] - b[1]));
    for (int idx = 0; idx < nums1.length && idx < k; idx++) {
      queue.offer(new int[] { nums1[idx], nums2[0], 0 });
    }
    while (k-- > 0 && !queue.isEmpty()) {
      int[] curr = queue.poll();
      List<Integer> temp = new ArrayList<>();
      temp.add(curr[0]);
      temp.add(curr[1]);
      result.add(temp);
      if (curr[2] == nums2.length - 1) {
        continue;
      }
      queue.add(new int[] { curr[0], nums2[curr[2] + 1], curr[2] + 1 });
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/632815975/){:target="_blank"}

# 설명
1. 주어진 배열 nums1과 nums2는 오름차순 정렬되어 있으며, 해당 값들을 이용하여 k개의 작은 부분 배열들을 만드는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- result는 부분 배열을 저장할 List이다.
- queue는 num1을 이용한 임의 부분 배열을 저장할 Queue로, $a[0] + a[1] - b[0] - b[1]$의 순서로 PriorityQueue를 이용하여 정의한다.

3. nums1을 반복하여 k개까지 조합을 queue에 넣어준다.
- 필요한 nums1의 값과 nums2의 첫 값, 0을 차례대로 queue에 넣어준다.

4. k를 감소시키며 0보다 크고 queue가 비어있지 않을 때 까지 반복하여 result에 부분 배열들을 넣어준다.
- curr에 queue의 배열을 꺼내 넣어준다.
- temp List를 새로 정의해서 curr의 앞의 두 값을 넣고 result에 넣어준다.
- curr의 세 번째 값이 $nums2.length - 1$인 경우, 반복을 계속 반복한다.
- queue에 curr의 첫 값과, nums2에서 curr의 세 번째 값에 1을 더한 값의 위치 값, curr의 세 번째 값에 1을 더한 값을 queue에 다시 넣어준다.

5. 반복이 완료되면 부분 배열을 넣은 reulst를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindKPairsWithSmallestSums.java){:target="_blank"}에서 확인 가능합니다.