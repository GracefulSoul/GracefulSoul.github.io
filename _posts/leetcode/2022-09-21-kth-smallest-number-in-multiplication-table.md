---
title: "Leetcode Java Kth Smallest Number in Multiplication Table"
excerpt: "Leetcode Kth Smallest Number in Multiplication Table Java"
last_modified_at: 2022-09-21T19:30:00
header:
  image: /assets/images/leetcode/kth-smallest-number-in-multiplication-table.png
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
[Link](https://leetcode.com/problems/kth-smallest-number-in-multiplication-table){:target="_blank"}

# 코드
```java
class Solution {

  public int findKthNumber(int m, int n, int k) {
    int left = 1;
    int right = m * n;
    while (left < right) {
      int mid = (left + right) / 2;
      int count = (mid / n) * n;
      for (int idx = (mid / n) + 1; idx <= m; idx++) {
        count += mid / idx;
      }
      if (count >= k) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }
    return left;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/805207808/){:target="_blank"}

# 설명
1. $m \times n$ 크기의 2차원 배열에서 k번째로 작은 값을 찾는 문제이다.
- mat[i][j] == $i \times j$를 만족한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- left는 배열의 최솟값인 1로 초기화한다.
- right는 배열의 최댓값인 $m \times n$으로 초기화한다.

3. left가 right보다 작을 때 까지 아래를 반복한다.
- mid는 중간 값을 넣을 변수로, $\frac{left + right}{2}$을 넣어준다.
- count는 현재 위치에서 작은 값의 수를 계산할 변수로, $\frac{mid}{n}$의 정수 값에 n을 곱해서 넣어준다.
- $\frac{mid}{n}$의 정수 값에 1을 더한 값부터 m 이하까지 idx를 증가시키며, count에 $\frac{mid}{idx}$ 값을 넣어준다.
- count가 k이상인 경우, right에 mid를 넣어 right보다 작은 숫자의 범위로 좁혀준다.
- count가 k미만인 경우, left에 $mid + 1$을 넣어 left보다 큰 숫자의 범위로 좁혀준다.

4. 반복이 완료되면 k번째로 작은 값인 left를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/KthSmallestNumberInMultiplicationTable.java){:target="_blank"}에서 확인 가능합니다.