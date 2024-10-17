---
title: "Leetcode Java Single Element in a Sorted Array"
excerpt: "Leetcode - 'Single Element in a Sorted Array' 문제 Java 풀이"
last_modified_at: 2022-06-22T20:00:00
header:
  image: /assets/images/leetcode/single-element-in-a-sorted-array.png
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
[Link](https://leetcode.com/problems/single-element-in-a-sorted-array/){:target="_blank"}

# 코드
```java
class Solution {

  public int singleNonDuplicate(int[] nums) {
    int start = 0;
    int end = nums.length - 1;
    while (start < end) {
      int mid = (start + end) / 2;
      if (mid % 2 == 1) {
        mid--;
      }
      if (nums[mid] == nums[mid + 1]) {
        start = mid + 2;
      } else {
        end = mid;
      }
    }
    return nums[start];
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/728387870/){:target="_blank"}

# 설명
1. nums 내 유일한 값을 찾는 문제이다.
- 단, O(log n) 시간과 O(1)의 공간 복잡도를 가진 방법으로 풀어야 한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- start는 num의 검색을 시작할 위치를 저장할 변수로, 0으로 정의한다.
- end는 num의 검색을 종료할 위치를 저장할 변수로, nums의 길이에 1을 빼서 정의한다.

3. start가 end 미만일 때 까지 반복하여 탐색을 수행한다.
- mid에 $\frac{start + end}{2}$의 결과를 넣어준다.
- 만일 mid가 홀수인 경우, mid를 감소시켜 짝수로 만들어 우측에 값이 반드시 존재하도록 만들어준다.
- num의 mid번째 값과 nums의 $mid + 1$번째 값이 동일한 경우, start에 $mid + 2$를 넣어 동일한 값까지 무시하고 시작 위치를 증가시켜 탐색 범위를 좁혀준다.
- num의 mid번째 값과 nums의 $mid + 1$번째 값이 다른 경우, end에 mid를 넣어 종료 위치를 감소시켜 탐색 범위를 좁혀준다.

4. 반복이 완료되면 탐색된 nums의 start번째 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SingleElementInASortedArray.java){:target="_blank"}에서 확인 가능합니다.