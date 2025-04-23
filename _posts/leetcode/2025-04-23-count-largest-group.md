---
title: "Leetcode Java Count Largest Group"
excerpt: "Leetcode - 'Count Largest Group' 문제 Java 풀이"
last_modified_at: 2025-04-23T19:35:00
header:
  image: /assets/images/leetcode/count-largest-group.png
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
[Link](https://leetcode.com/problems/count-largest-group/){:target="_blank"}

# 코드
```java
class Solution {

  public int countLargestGroup(int n) {
    int[] counts = new int[37];
    int result = 0;
    int max = 0;
    for (int i = 1; i <= n; i++) {
      int sum = 0;
      for (int x = i; x > 0; x /= 10) {
        sum += x % 10;
      }
      counts[sum]++;
      if (max == counts[sum]) {
        result++;
      } else if (max < counts[sum]) {
        max = counts[sum];
        result = 1;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-largest-group/submissions/1615556804/){:target="_blank"}

# 설명
1. [1, n] 범위 내 값들 중 각 자리 숫자의 합이 동일한 숫자들끼리 그룹을 만들 때, 가장 많은 숫자가 모인 그룹의 갯수를 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- counts는 합계가 동일한 숫자의 갯수를 계산할 변수로, 합이 최대인 9999의 합인 $9 \times 4 = 36$ 보다 1 큰 37 크기의 정수 배열로 초기화한다.
- result는 가장 많은 숫자가 모인 그룹의 갯수를 계산할 변수로, 0으로 초기화한다.
- max는 가장 많은 숫자가 모인 그룹의 크기를 저장할 변수로, 0으로 초기화한다.

3. 1부터 n 이하까지 i를 증가시키며 아래를 반복한다.
- sum은 각 숫자의 합계를 더할 변수로, 현재 숫자 i의 각 숫자 합을 더한 값을 넣어준다.
- counts[sum]의 갯수를 증가시켜준다.
- max와 counts[sum]의 값이 동일한 경우, result를 증가시켜 갯수를 더해준다.
- max보다 counts[sum]의 값이 큰 경우, max에 counts[sum]을 넣어 새로운 최댓값으로 설정하고 result를 1로 초기화한다.

4. 반복이 완료되면 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountLargestGroup.java){:target="_blank"}에서 확인 가능합니다.