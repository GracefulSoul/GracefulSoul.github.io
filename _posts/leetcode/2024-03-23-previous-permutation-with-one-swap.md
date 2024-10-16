---
title: "Leetcode Java Previous Permutation With One Swap"
excerpt: "Leetcode Previous Permutation With One Swap Java"
last_modified_at: 2024-03-23T11:50:00
header:
  image: /assets/images/leetcode/previous-permutation-with-one-swap.png
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
[Link](https://leetcode.com/problems/previous-permutation-with-one-swap/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] prevPermOpt1(int[] arr) {
    int i = arr.length - 2;
    int j = arr.length - 1;
    while (i >= 0 && arr[i] <= arr[i + 1]) {
      i--;
    }
    if (i < 0) {
      return arr;
    }
    while (arr[j] >= arr[i] || (j > 0 && arr[j] == arr[j - 1])) {
      j--;
    }
    int temp = arr[j];
    arr[j] = arr[i];
    arr[i] = temp;
    return arr;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/previous-permutation-with-one-swap/submissions/1211315378/){:target="_blank"}

# 설명
1. arr 내 한 번의 값 변경을 통해서 arr보다 사전적으로 작지만 사전적으로 가장 큰 배열을 반환하는 문제이다.
- 단, 불가능한 경우 arr 그대로 반환한다.

2. i와 j는 값의 변경을 위한 위치 변수로, 마지막의 두 위치를 순차적으로 넣어준다.

3. i가 0보다 크면서 다음 값보다 클 때 까지 i를 감소시킨다.

4. i가 0보다 작으면 구성이 불가능하므로, arr을 반환한다.

5. arr의 j번째 값이 i번째 값보다 크거나, j가 0보다 크고 이전 위치와 동일할 때 까지 j를 감소시킨다.

6. i와 j의 위치가 결정되면 두 값의 위치를 바꾼 arr을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/PreviousPermutationWithOneSwap.java){:target="_blank"}에서 확인 가능합니다.