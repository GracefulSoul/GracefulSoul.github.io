---
title: "Leetcode Java Minimized Maximum of Products Distributed to Any Store"
excerpt: "Leetcode - 'Minimized Maximum of Products Distributed to Any Store' 문제 Java 풀이"
last_modified_at: 2024-11-14T18:30:00
header:
  image: /assets/images/leetcode/minimized-maximum-of-products-distributed-to-any-store.png
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
[Link](https://leetcode.com/problems/minimized-maximum-of-products-distributed-to-any-store/){:target="_blank"}

# 코드
```java
class Solution {

  public int minimizedMaximum(int n, int[] quantities) {
    int left = 1;
    int right = 100000;
    while (left < right) {
      int mid = (left + right) / 2;
      int sum = 0;
      for (int quantity : quantities) {
        sum += (quantity + (mid - 1)) / mid;
      }
      if (sum > n) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return left;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimized-maximum-of-products-distributed-to-any-store/submissions/1452431630/){:target="_blank"}

# 설명
1. 제품 유형 별 갯수가 저장된 quantities를 n개 상점에 아래의 규칙대로 배포할때, 배포할 수 있는 최대 가능한 갯수를 반환하는 문제이다.
- 각 상점에는 한 가지 유형의 제품만 취급 가능하다.
- 각 상점에 제공하는 제품 갯수는 최소화하여 제공해야한다.

2. left와 right는 quantities의 탐색 위치를 저장할 변수로, 제품 유형의 범위인 1과 100000으로 초기화한다.

3. left가 right 미만일 때 까지 아래를 반복한다.
- mid는 중앙값을 저장할 변수로, $\frac{left + right}{2}$의 값으로 초기화한다.
- sum은 제품의 합계를 저장할 변수로, quantities를 반복하여 $\frac{quantity + (mid - 1)}{mid}$인 mid개씩 제품을 분배할 때 가능한 상점의 수를 계산한다.
- 위의 반복이 완료되면 sum이 n보다 큰 경우, left에 $mid + 1$을 아니면 right에 mid를 넣어 제품 분배 갯수를 조절한다.

4. 반복이 완료되면 분배 갯수가 저장된 left를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimizedMaximumOfProductsDistributedToAnyStore.java){:target="_blank"}에서 확인 가능합니다.