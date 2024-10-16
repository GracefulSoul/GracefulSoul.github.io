---
title: "Leetcode Java Unique Binary Search Trees"
excerpt: "Leetcode Unique Binary Search Trees Java 풀이"
last_modified_at: 2021-07-16T18:00:00
header:
  image: /assets/images/leetcode/unique-binary-search-trees.png
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
[Link](https://leetcode.com/problems/unique-binary-search-trees/){:target="_blank"}

# 코드
```java
class Solution {

  public int numTrees(int n) {
    int[] dp = new int[n + 1];
    dp[0] = 1;
    dp[1] = 1;
    for (int i = 2; i <= n; i++) {
      for (int j = 1; j <= i; j++) {
        dp[i] += dp[i - j] * dp[j - 1];
      }
    }
    return dp[n];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/523342275/){:target="_blank"}

# 설명
1. 주어진 정수 n을 이용해서 [이진 트리](https://en.wikipedia.org/wiki/Binary_tree){:target="_blank"}를 구성하는 경우의 수를 구하는 문제이다.

2. 문제 풀이를 위해 dp를 주어진 정수인 n보다 1 크게 정의하고, 0과 1 자리에 1을 넣어 초기화 시킨다.

3. i는 dp의 초기화 되지 않은 2번째 자리에서 n까지 값을 증가시키며 반복한다.

4. j는 1부터 i까지 증가시키며 반복한다.

5. dp[n]을 구하기 위한 값을 풀어보면 아래와 같다.
- $dp[2] = dp[0] * dp[1] + dp[1] * dp[0] = 2$
- $dp[3] = dp[0] * dp[2] + dp[1] * dp[1] + dp[1] + dp[2] * dp[0] = 5$
- $dp[n] = dp[0] * dp[n - 1] + dp[1] * dp[n - 2] + ... + $
  $dp[n - 2] * dp[1] + dp[n - 1] * dp[0]$
- 위의 식대로 풀이해보면, 3번과 4번의 반복을 수행하여 $dp[i] += dp[i - j] * dp[j - 1]$로 dp[i]의 값을 넣어준다.

6. 반복이 완료되면 완성된 dp의 n번째 값인 dp[n]의 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/UniqueBinarySearchTrees.java){:target="_blank"}에서 확인 가능합니다.