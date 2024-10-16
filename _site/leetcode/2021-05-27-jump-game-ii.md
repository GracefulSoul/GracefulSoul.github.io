---
title: "Leetcode Java Jump Game II"
excerpt: "Leetcode Jump Game II Java 풀이"
last_modified_at: 2021-05-26T17:00:00
header:
  image: /assets/images/leetcode/jump-game-ii.png
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
[Link](https://leetcode.com/problems/jump-game-ii/){:target="_blank"}

# 코드
```java
class Solution {

  public int jump(int[] nums) {
    int count = 0;
    int target = 0;
    int max = 0;
    for (int idx = 0; idx < nums.length - 1; idx++) {
      max = Math.max(max, idx + nums[idx]);
      if (idx == target) {
        count++;
        target = max;
      }
      if (target == nums.length - 1) {
        break;
      }
    }
    return count;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/498893061/){:target="_blank"}

# 설명
1. 최소의 점프로 배열의 마지막 자리에 도달하기 위한 횟수를 구하는 문제이다.

2. 반복을 통해서 마지막 자리에 도달하기 위한 최소 점프 횟수를 구한다.
- 목표가 되는 지점이 가장 먼 지점으로 갈 수 있는 max를 구하기 위해 max와 점프 길이인 idx + nums[idx] 중 큰 값을 max에 주입한다.
- idx가 목표 지점인 target인 경우, 점프 횟수인 count를 증가시키고 target에 다음 목표 지점인 max를 주입한다.

3. 목표 지점인 target이 주어진 배열 nums의 마지막 값의 위치인 $nums.length - 1$인 경우, 반복을 종료한다.

4. 반복이 종료되면 점프 횟수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/JumpGameII.java){:target="_blank"}에서 확인 가능합니다.