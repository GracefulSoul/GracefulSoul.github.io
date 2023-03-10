---
title: "Leetcode Java Set Mismatch"
excerpt: "Leetcode Set Mismatch Java"
last_modified_at: 2022-09-02T18:40:00
header:
  image: /assets/images/leetcode/set-mismatch.png
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
[Link](https://leetcode.com/problems/set-mismatch/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] findErrorNums(int[] nums) {
    int[] count = new int[nums.length + 1];
    int[] result = new int[2];
    for (int num : nums) {
      count[num]++;
    }
    for (int idx = 0; idx < count.length; idx++) {
      switch (count[idx]) {
        case 0: result[1] = idx; break;
        case 2: result[0] = idx; break;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/789524318/){:target="_blank"}

# 설명
1. nums 내 중복된 값과 빠진 값 순으로 배열로 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- count는 nums의 개수를 구하기 위한 배열로, nums의 길이보다 1 큰 정수 배열로 초기화한다.
- result는 중복된 값과 빠진 값을 반환하기 위한 배열로, 2 크기의 정수 배열로 초기화한다.

3. nums를 반복하여 count의 num번째 위치값을 증가시킨다.

4. 0부터 count의 길이 미만까지 아래를 반복한다.
- count의 idx번째 값이 0이면 빠진 값이므로, result의 두 번째 값을 idx로 넣어준다.
- count의 idx번째 값이 2이면 중복된 값이므로, result의 첫 번째 값을 idx로 넣어준다.

5. 중복된 값과 빠진 값 순서로 저장한 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SetMismatch.java){:target="_blank"}에서 확인 가능합니다.