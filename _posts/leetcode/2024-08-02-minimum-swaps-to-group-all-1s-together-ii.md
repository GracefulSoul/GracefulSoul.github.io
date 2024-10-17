---
title: "Leetcode Java Minimum Swaps to Group All 1's Together II"
excerpt: "Leetcode Medium - 'Minimum Swaps to Group All 1's Together II' 문제 Java 풀이"
last_modified_at: 2024-08-02T19:20:00
header:
  image: /assets/images/leetcode/minimum-swaps-to-group-all-1s-together-ii.png
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
[Link](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int minSwaps(int[] nums) {
    int length = nums.length;
    int ones = 0;
    for (int num : nums) {
      if (num == 1) {
        ones++;
      }
    }
    int max = 0;
    for (int i = 0, count = 0; i < length + ones; i++) {
      if (i >= ones && nums[i - ones] == 1) {
        count--;
      }
      if (nums[i % length] == 1) {
        count++;
      }
      max = Math.max(max, count);
    }
    return ones - max;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together-ii/submissions/1341703981/){:target="_blank"}

# 설명
1. nums 내 1의 값들을 각자 뭉쳐있게 재배치하기 위한 최소 이동 횟수를 구하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 nums의 길이를 저장한 변수이다.
- ones는 nums내 1의 갯수를 저장할 변수로, nums를 반복하여 1의 갯수를 넣어준다.
- max는 [Sliding Window](https://en.wikipedia.org/wiki/Sliding_window_protocol){:target="_blank"} 방식으로 Window 내 1의 최대 갯수를 저장할 변수로, 0으로 초기화한다.

3. 0부터 length 미만까지 i를 증가시키며, 범위 내 1의 갯수인 count는 0으로 초기화하여 아래를 반복한다.
- i가 ones 이상이면서 nums[$i - ones$]의 값이 1인 연결된 1의 갯수가 ones와 동일한 경우, count를 감소시켜준다.
- nums의 $\frac{i}{length}$의 나머지 값에 해당하는 값이 1인 Window 내 1의 갯수가 증가하는 경우, count를 증가시켜준다.
- max에 max와 count 중 큰 값인 Window 내 1의 최대 갯수를 넣어준다.

4. 반복이 완료되면 조건을 만족하기 위해 1과 0을 스왑해야 하는 최소 횟수인 $ones - max$를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimumSwapsToGroupAll1sTogetherII.java){:target="_blank"}에서 확인 가능합니다.