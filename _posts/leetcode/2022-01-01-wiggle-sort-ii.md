---
title: "Leetcode Java Wiggle Sort II"
excerpt: "Leetcode Wiggle Sort II Java 풀이"
last_modified_at: 2021-12-31T13:00:00
header:
  image: /assets/images/leetcode/wiggle-sort-ii.png
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
[Link](https://leetcode.com/problems/wiggle-sort-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public void wiggleSort(int[] nums) {
    int length = nums.length;
    if (length == 1) {
      return;
    }
    int[] count = new int[5001];
    for (int num : nums) {
      count[num]++;
    }
    int j = 1;
    for (int i = 5000; i >= 0; i--) {
      while (count[i] > 0) {
        nums[j] = i;
        count[i]--;
        j += 2;
        if (j >= length) {
          j = 0;
        }
      }
    }
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/610662377/){:target="_blank"}

# 설명
1. 주어진 배열 nums를 이용하여 아래의 조건을 만족하는 배열로 변환하는 문제이다.
- 배열 내 값들은 nums[0] < nums[1] > nums[2] < nums[3] ... 와 같이 특정 위치의 값은 좌측의 값보다 커야하고, 우측 값보다 작아야한다.
- O(1)의 시간 복잡도 또는 [In-Place 알고리즘](https://en.wikipedia.org/wiki/In-place_algorithm){:target="_blank"}으로 O(n)의 여분 공간으로 풀이하는 것을 요구한다.

2. length에 nums의 길이를 넣어주고, length가 1인 경우 정렬이 필요하지 않으므로 반환한다.

3. 숫자를 넣을 count 배열을 정의하고, nums 내 값의 범위인 0 ~ 5000까지 값을 세기 위해 5001 크기로 초기화한다.

4. nums를 순회하여 count 배열에 num번째 값을 증가시킨다.

5. j를 1로 정의하고, 5000부터 0까지 i를 감소시키며 nums의 값을 변경시켜준다.
- count[i]의 값이 0보다 큰 경우, 아래를 수행한다.
  - nums의 j번째 위치에 i를 넣어주고, count의 i번째 값을 감소시킨다.
  - j를 2 증가시키고, j가 length보다 큰 경우 0으로 초기화한다.
- 위의 방식대로 반복을 계속하여 큰 수를 nums의 홀수 위치에 차례대로 넣고, 작은 수를 다시 앞에서부터 nums의 0을 포함한 짝수 위치에 차례대로 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/WiggleSortII.java){:target="_blank"}에서 확인 가능합니다.