---
title: "Leetcode Java K-th Smallest Prime Fraction"
excerpt: "Leetcode - 'K-th Smallest Prime Fraction' 문제 Java 풀이"
last_modified_at: 2022-12-29T10:20:00
header:
  image: /assets/images/leetcode/k-th-smallest-prime-fraction.png
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
[Link](https://leetcode.com/problems/k-th-smallest-prime-fraction){:target="_blank"}

# 코드
```java
class Solution {

  public int[] kthSmallestPrimeFraction(int[] arr, int k) {
    Queue<int[]> queue = new PriorityQueue<int[]>((a, b) -> arr[a[0]] * arr[b[1]] - arr[a[1]] * arr[b[0]]);
    for (int idx = 1; idx < arr.length; idx++) {
      queue.add(new int[] { 0, idx });
    }
    while (--k > 0) {
      int[] fraction = queue.poll();
      if (fraction[0]++ < fraction[1]) {
        queue.add(fraction);
      }
    }
    int[] result = queue.poll();
    return new int[] { arr[result[0]], arr[result[1]] };
  }

}
```

# 결과
[Link](https://leetcode.com/problems/k-th-smallest-prime-fraction/submissions/867224667/){:target="_blank"}

# 설명
1. arr은 아래의 규칙으로 이루어진 분수 표현법을 적용할 경우 k번째 작은 값을 찾는 문제이다.
- 배열 arr의 첫 값은 '1'이며, 양의 정수로 이루어져있다.
- 배열 arr의 값은 [i, ..., j]로 이루어져 있으며, $0 <= i < j < arr.length$를 만족한다.
- arr은 $frac{i}{j}$의 분수로 표현 가능하며, 결과 값인 answer은 [arr[i], arr[j]] 형태의 정수 배열로 반환한다.

2. queue는 작은 분수 값이 가장 앞에 위치하도록 각 값의 위치 정보를 저장할 변수로, 아래의 정렬을 기반으로 한 PriorityQueue로 초기화한다.
- queue 내 정수 배열 a와 b를 arr을 이용해 더 작은 값이 맨 앞으로 위치하도록 아래의 두 값의 차이가 큰 수가 앞으로 나오게 정렬하게 한다.
  - arr에서 a의 분자에 해당하는 a의 첫 번째 값과 b의 분모에 해당하는 b의 두 번째 값의 곱.
  - arr에서 a의 분모에 해당하는 a의 두 번째 값과 b의 분자에 해당하는 b의 첫 번째 값의 곱.

3. queue에 1부터 arr의 길이 미만까지 반복하여, [1, idx] 형태로 arr의 위치 값을 배열로 넣어준다.

4. k를 감소시키고 0보다 클 때 까지 아래를 수행한다.
- fraction을 queue에서 가장 작은 값을 꺼내 넣어준다.
- faction의 첫 번째 값을 증가시켰을 경우, 두 번째 값보다 작으면 1 미만의 값이므로 queue에 다시 faction을 넣어준다.

5. 반복이 완료되면 result에 k번째 작은 분수의 값을 표현할 값을 queue에서 꺼내 넣어주고, 주어진 문제의 결과로 arr에서 result의 첫 번째 값과 result의 두 번째 값을 배열로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KthSmallestPrimeFraction.java){:target="_blank"}에서 확인 가능합니다.