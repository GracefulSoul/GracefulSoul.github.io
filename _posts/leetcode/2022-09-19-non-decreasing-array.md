---
title: "Leetcode Java Non-decreasing Array"
excerpt: "Leetcode - 'Non-decreasing Array' 문제 Java 풀이"
last_modified_at: 2022-09-19T11:30:00
header:
  image: /assets/images/leetcode/non-decreasing-array.png
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
[Link](https://leetcode.com/problems/non-decreasing-array){:target="_blank"}

# 코드
```java
class Solution {

  public boolean checkPossibility(int[] nums) {
    int count = 0;
    for (int idx = 1; idx < nums.length && count <= 1; idx++) {
      if (nums[idx - 1] > nums[idx]) {
        count++;
        if (idx - 2 < 0 || nums[idx - 2] <= nums[idx]) {
          nums[idx - 1] = nums[idx];
        } else {
          nums[idx] = nums[idx - 1];
        }
      }
    }
    return count <= 1;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/803548824/){:target="_blank"}

# 설명
1. nums의 값을 최대 하나만 수정하여 감소하지 않는 배열을 만들 수 있는지 검증하는 문제이다.
- 0 <= i <= $n - 2$ 처럼 모든 i에 대해 num[i] <= nums[$i + 1$]이 유지되는 경우 배열이 감소하지 않는 배열이라고 한다.

2. count는 수정 횟수를 계산할 변수로, 0으로 초기화한다.

3. 1부터 nums의 길이 미만이고 count가 1 이하일 때 까지 idx를 증가시키며 아래를 반복한다.
- nums의 $idx - 1$번째 값이 idx보다 큰 경우, 값을 수정해야하므로 아래를 수행한다.
  - 수정 횟수인 count를 증가시킨다.
  - $idx - 2$가 0보다 작거나 nums의 $idx - 2$번째 값이 idx번째 값과 같거나 작은 경우, nums의 $idx - 1$ 위치에 idx번째 값을 넣어준다.
  - 위의 경우가 아니라면, nums의 idx번째 위치에 $idx - 1$번째 값을 넣어준다.

4. 반복이 완료되면 수정 횟수가 1 이하인지 검증한 결과를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/NonDecreasingArray.java){:target="_blank"}에서 확인 가능합니다.