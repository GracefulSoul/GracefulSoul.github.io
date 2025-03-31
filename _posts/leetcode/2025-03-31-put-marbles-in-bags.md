---
title: "Leetcode Java Put Marbles in Bags"
excerpt: "Leetcode - 'Put Marbles in Bags' 문제 Java 풀이"
last_modified_at: 2025-03-31T18:50:00
header:
  image: /assets/images/leetcode/put-marbles-in-bags.png
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
[Link](https://leetcode.com/problems/put-marbles-in-bags/){:target="_blank"}

# 코드
```java
class Solution {

  public long putMarbles(int[] weights, int k) {
    int length = weights.length;
    int[] sum = new int[length - 1];
    for (int i = 0; i < sum.length; i++) {
      sum[i] = weights[i] + weights[i + 1];
    }
    Arrays.sort(sum);
    long result = 0;
    for (int i = 0; i < k - 1; i++) {
      result += sum[length - 2 - i] - sum[i];
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/put-marbles-in-bags/submissions/1591866821/){:target="_blank"}

# 설명
1. k개의 가방과 각 대리석의 갯수가 담긴 weights를 이용하여 아래의 조건에 따른 최댓값과 최솟값의 차이를 구하는 문제이다.
- 가방은 비어있지 않는다.
- i번째 대리석과 j번째 대리석이 동일한 가방안에 있다면, 그 사이 대리석들도 가방 안에 있으며 무게는 $weights[i] + weights[j]$가 된다.
- 구슬을 가방 별로 나눈 후 점수는 각 가방 무게의 합이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 weights의 길이를 저장한 변수이다.
- sum은 합계를 저장할 변수로, $length - 1$ 크기의 정수 배열로 초기화하고 인접한 두 값의 합을 순차적으로 저장하고 오름차순 정렬한다.
- result는 결과를 저장할 변수로, 0으로 초기화한다.

3. 0부터 $k - 1$인 가방의 갯수만큼 i를 증가시키며 아래를 반복한다.
- result에 sum의 $length - 2 - i$번째 값에서 i번째 값을 뺀 가방에 들어갈 대리석의 숫자를 더해준다.

4. 반복이 완료되면 결과가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PutMarblesInBags.java){:target="_blank"}에서 확인 가능합니다.