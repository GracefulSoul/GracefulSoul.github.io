---
title: "Leetcode Java Max Chunks To Make Sorted II"
excerpt: "Leetcode Max Chunks To Make Sorted II Java"
last_modified_at: 2022-12-18T10:30:00
header:
  image: /assets/images/leetcode/max-chunks-to-make-sorted-ii.png
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
[Link](https://leetcode.com/problems/max-chunks-to-make-sorted-ii){:target="_blank"}

# 코드
```java
class Solution {

  public int maxChunksToSorted(int[] arr) {
    int length = arr.length;
    int[] dp = new int[length];
    dp[0] = arr[0];
    for (int idx = 1; idx < length; idx++) {
      dp[idx] = Math.max(dp[idx - 1], arr[idx]);
    }
    int result = 1;
    int min = arr[length - 1];
    for (int idx = length - 2; idx >= 0; idx--) {
      if (dp[idx] <= min) {
        result++;
      }
      min = Math.min(min, arr[idx]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/max-chunks-to-make-sorted-ii/submissions/861378708/){:target="_blank"}

# 설명
1. arr내 부분 배열로 나눌 때, 부분 배열을 각각 정렬해서 이어준 결과와 기존 배열을 정렬한 결과가 동일하기 위한 최대 부분 배열의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 arr의 길이를 저장한 변수이다.
- dp는 arr의 좌측부터 현재 위치까지 최대 값을 저장하기 위한 배열로, arr의 좌측부터 우측까지 이동하며 현재 위치까지의 최댓 값을 위치 별 저장한다.
- result는 부분 배열의 수를 저장하기 위한 변수로, 최소 개수인 1로 초기화한다.
- min은 최솟값을 저장할 변수로, arr의 마지막 값을 넣어준다.

3. $length - 2$부터 0 이상까지 idx를 감소시키며, 우측에서 좌측으로 이동하며 아래를 반복한다.
- dp의 idx번째 값이 min보다 작거나 같은 경우, 부분 배열의 수인 result를 증가시켜준다.
  - 위를 만족하는 경우, 우측으로 점층적으로 증가하는 오름차순 정렬을 만족한다.
  - 그렇기 때문에 최대 부분 배열의 수를 만족하기 위해서 한 숫자 씩 분리해서 부분 배열로 저장시키는 것이다.
- min에 현재 위치까지 가장 작은 수를 넣어 준다.

4. 반복이 완료되면 최대 부분 배열의 수를 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxChunksToMakeSortedII.java){:target="_blank"}에서 확인 가능합니다.