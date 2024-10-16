---
title: "Leetcode Java XOR Queries of a Subarray"
excerpt: "Leetcode XOR Queries of a Subarray Java"
last_modified_at: 2024-09-13T18:00:00
header:
  image: /assets/images/leetcode/xor-queries-of-a-subarray.png
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
[Link](https://leetcode.com/problems/xor-queries-of-a-subarray/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] xorQueries(int[] arr, int[][] queries) {
    int[] result = new int[queries.length];
    for (int i = 1; i < arr.length; i++) {
      arr[i] ^= arr[i - 1];
    }
    for (int i = 0; i < queries.length; i++) {
      int[] query = queries[i];
      result[i] = query[0] > 0 ? arr[query[0] - 1] ^ arr[query[1]] : arr[query[1]];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/xor-queries-of-a-subarray/submissions/1388285611/){:target="_blank"}

# 설명
1. arr 내 값들을 이용하여 queries 범위에 해당하는 숫자들의 XOR 값을 반환하는 문제이다.

2. result는 결과를 저장할 변수로, queries의 길이 크기의 정수 배열로 초기화 후 arr의 우측 값으로 이동하면서 좌측 값과의 XOR 결과를 순차적으로 넣어준다.

3. 0부터 queries의 길이 미만까지 i를 증가시키며 아래를 수행한다.
- query에 queries[i] 값을 꺼내 넣어준다.
- result[i]에 경우에 따라 해당하는 값을 넣어준다.
  - query[0]인 시작 위치가 0인 경우, 이미 XOR 연산을 누계한 arr[query[1]]의 값을 넣어준다.
  - 위의 경우가 아니라면 누계된 arr[query[1]]의 값에서 시작 위치 이전까지 누계된 값인 arr[$query[0] - 1$] 값을 XOR 연산한 결과를 넣어준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/XORQueriesOfASubarray.java){:target="_blank"}에서 확인 가능합니다.