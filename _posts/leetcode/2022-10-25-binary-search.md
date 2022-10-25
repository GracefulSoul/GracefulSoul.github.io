---
title: "Leetcode Java Binary Search"
excerpt: "Leetcode Binary Search Java"
last_modified_at: 2022-10-25T19:40:00
header:
  image: /assets/images/leetcode/binary-search.png
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
[Link](https://leetcode.com/problems/binary-search){:target="_blank"}

# 코드
```java
class Solution {

  public int search(int[] nums, int target) {
    int left = 0;
    int right = nums.length - 1;
    while (left <= right) {
      int mid = left + ((right - left) / 2);
      if (nums[mid] > target) {
        right = mid - 1;
      } else if (nums[mid] < target) {
        left = mid + 1;
      } else {
        return mid;
      }
    }
    return -1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/829881102/){:target="_blank"}

# 설명
1. 기초적인 [Binary Search Algorithm](https://en.wikipedia.org/wiki/Binary_search_algorithm){:target="_blank"}을 수행하는 문제이다.
- 단, 탐색 결과가 없을 경우 -1을 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- left는 좌측 탐색 범위를 제한할 변수로, 0으로 초기화한다.
- right는 우측 탐색 범위를 제한할 변수로, nums의 길이보다 1 작게 정의한다.

3. left가 right보다 작거나 같을 때 까지 아래의 이진 탐색을 수행한다.
- mid는 이진 탐색의 중위값을 정의할 변수로, $\frac{right - left}{2}$에 left를 더해 넣어준다.
- nums의 mid번째 값이 target보다 큰 경우, 우측의 범위를 좁혀야 하므로 right에 $mid - 1$을 넣어준다.
- nums의 mid번째 값이 target보다 작은 경우, 좌측의 범위를 좁혀야 하므로 left에 $mid + 1$을 넣어준다.
- 그 외의 경우인 nums의 mid번째 값이 target인 경우, 원하는 값의 위치를 찾았으므로 mid를 주어진 문제의 결과로 반환한다.

4. 반복이 완료되면 탐색 결과가 없으므로, -1을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/BinarySearch.java){:target="_blank"}에서 확인 가능합니다.