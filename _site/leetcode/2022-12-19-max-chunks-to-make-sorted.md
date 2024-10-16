---
title: "Leetcode Java Max Chunks To Make Sorted"
excerpt: "Leetcode Max Chunks To Make Sorted Java"
last_modified_at: 2022-12-19T11:40:00
header:
  image: /assets/images/leetcode/max-chunks-to-make-sorted.png
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
[Link](https://leetcode.com/problems/max-chunks-to-make-sorted){:target="_blank"}

# 코드
```java
class Solution {

  public int maxChunksToSorted(int[] arr) {
    int max = 0;
    int result = 0;
    for (int idx = 0; idx < arr.length; idx++) {
      max = Math.max(max, arr[idx]);
      if (max == idx) {
        result++;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/max-chunks-to-make-sorted-ii/submissions/861378708/){:target="_blank"}

# 설명
1. 지난 번 [Max Chunks To Make Sorted II](max-chunks-to-make-sorted-ii){:target="_blank"}와 비슷한 문제로 [0, n - 1] 범위의 길이 n의 정수 배열인 arr을 부분 배열로 나눌 때, 부분 배열을 각각 정렬해서 이어준 결과와 기존 배열을 정렬한 결과가 동일하기 위한 최대 부분 배열의 수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- max는 최댓 값을 저장할 변수로, 0으로 초기화한다.
- result는 최대 부분 배열의 수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 arr의 길이 전까지 idx를 증가시키며 아래를 반복한다.
- max에 현재 위치까지 가장 큰 값을 임시 저장시킨다.
- max와 idx가 동일하면 정렬된 위치와 같아 하나의 부분 배열로 분리 가능하므로, result를 증가시킨다.

4. 반복이 완료되면 최대 부분 배열의 수가 저장된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaxChunksToMakeSorted.java){:target="_blank"}에서 확인 가능합니다.