---
title: "Leetcode Java Minimum Moves to Equal Array Elements II"
excerpt: "Leetcode Minimum Moves to Equal Array Elements II Java 풀이"
last_modified_at: 2022-04-21T12:00:00
header:
  image: /assets/images/leetcode/minimum-moves-to-equal-array-elements-ii.png
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
[Link](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int minMoves2(int[] nums) {
    Arrays.sort(nums);
    int left = 0;
    int right = nums.length - 1;
    int move = 0;
    while (left < right) {
      move += nums[right--] - nums[left++];
    }
    return move;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/684494857/){:target="_blank"}

# 설명
1. nums 배열내 모든 요소의 값을 동일하게 만들기 위한 횟수를 구하는 문제이다.
- 한 번에 배열의 한 요소를 1씩 증가 혹은 감소시킬 수 있다.

2. 문제 풀이 전 nums 배열 내 값들을 오름차순으로 정렬해준다.

3. 문제 풀이에 필요한 변수를 정의한다.
- left는 정렬된 nums의 작은 값부터 탐색하기 위한 변수로, 0으로 초기화한다.
- right는 정렬된 nums의 큰 값부터 탐색하기 위한 변수로, nums의 길이보다 1 작게 초기화한다.
- move는 nums 배열 내 모든 요소의 값을 동일하게 만들기 위한 횟수를 저장하기 위한 변수로, 0으로 초기화한다.

4. left가 right보다 작을 때 까지 반복하여 아래를 수행한다.
- move에 nums의 right번째 값과 left번째 값의 차이를 더해서 배열 내 값을 동일하게 만들기 위한 증감 폭을 계산한다.
- right를 감소시키고, left를 증가시킨 후 반복을 계속 수행한다.

5. 반복이 완료되면 계산된 횟수인 move를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumMovesToEqualArrayElementsII.java){:target="_blank"}에서 확인 가능합니다.