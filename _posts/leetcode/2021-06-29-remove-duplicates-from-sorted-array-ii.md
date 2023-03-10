---
title: "Leetcode Java Remove Duplicates from Sorted Array II"
excerpt: "Leetcode Remove Duplicates from Sorted Array II Java 풀이"
last_modified_at: 2021-06-29T18:00:00
header:
  image: /assets/images/leetcode/remove-duplicates-from-sorted-array-ii.png
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
[Link](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int removeDuplicates(int[] nums) {
    int count = 0;
    for (int n : nums) {
      if (count < 2 || n > nums[count - 2]) {
        nums[count++] = n;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/514817750/){:target="_blank"}

# 설명
1. 주어진 배열 nums는 오름차순 된 정수를 담은 배열로, 2번 초과로 동일한 숫자가 나오지 않는 배열로 만들고 해당 위치를 반환하는 문제이다.
- 단, 주어진 배열 nums를 그대로 사용하여 변경해야하므로 [In-Place 알고리즘](https://en.wikipedia.org/wiki/In-place_algorithm){:target="_blank"}을 이용하여 변경해야 한다.

2. 주어진 배열을 만들고 마지막 위치를 저장할 count 변수를 선언한다.

3. nums를 반복하여 2번 초과로 동일한 숫자가 나오지 않는 배열을 만들고 위치를 계산한다.
- 2번 초과로 동일한 숫자가 나오지 않도록 아래의 두 경우를 고려하여 해당 위치에 그대로 값을 넣어준다.
  - 2번 이상까지 반복이 허용되므로, nums[count - 2]번째 값보다 n이 커야한다.
  - 위의 경우를 생각해보면 처음 두 값은 동일한 값이 와도 상관이 없다.
    - 다음 값을 넣을 때 확인이 되므로, 처음 두 값은 확인하지 않아도 된다.

4. 반복이 종료되면 새롭게 값을 넣은 nums의 마지막 위치 값이자, 새로 정렬된 숫자의 개수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RemoveDuplicatesFromSortedArrayII.java){:target="_blank"}에서 확인 가능합니다.