---
title: "Leetcode Java Find K Closest Elements"
excerpt: "Leetcode Find K Closest Elements Java"
last_modified_at: 2022-09-14T19:30:00
header:
  image: /assets/images/leetcode/find-k-closest-elements.png
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
[Link](https://leetcode.com/problems/find-k-closest-elements){:target="_blank"}

# 코드
```java

class Solution {

  public List<Integer> findClosestElements(int[] arr, int k, int x) {
    int left = 0;
    int right = arr.length - k;
    while (left < right) {
      int mid = left + ((right - left) / 2);
      if (x - arr[mid] > arr[mid + k] - x) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    List<Integer> result = new ArrayList<>(k);
    for (int idx = 0; idx < k; idx++) {
      result.add(arr[left + idx]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/799537758/){:target="_blank"}

# 설명
1. arr 배열의 x에 가까운 k개의 정수를 반환하는 문제이다.
- 아래 중 하나의 경우라도 만족하면 a는 b보다 x에 가깝다.
  - \|a - x\| < \|b - x\|인 경우.
  - \|a - x\| == \|b - x\|이고 a < b인 경우.

2. 문제 풀이에 필요한 변수를 정의한다.
- left는 배열의 좌측 탐색 위치를 저장하기 위한 변수로, 첫 위치인 0으로 초기화한다.
- right는 배열의 우측 탐색 위치를 저장하기 위한 변수로, 연속된 k를 골라야하므로 arr 길이보다 k 작은 값으로 초기화한다.

3. left가 right보다 작을 때 까지 아래를 반복한다.
- mid에 x에 가까운 위치를 추정하기 위해 $left + \frac{right - left}{2}$를 넣어준다.
- $x - arr[mid]$가 $arr[mid + k] - x$보다 큰 경우 arr[mid]가 x에 가까우므로, left에 $mid + 1$을 넣어 범위를 좁혀준다.
- 위의 경우가 아니면 arr[mid + k]가 x에 가깝거나 동일한 위치이므로, right에 mid를 넣어 범위를 좁혀준다.

4. 반복이 완료되면 결과를 넣을 result를 k 크기의 ArrayList로 초기화하고, arr[left] 값부터 우측으로 k개를 result에 넣어 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/FindKClosestElements.java){:target="_blank"}에서 확인 가능합니다.