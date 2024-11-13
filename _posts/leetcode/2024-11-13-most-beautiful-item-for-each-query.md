---
title: "Leetcode Java Most Beautiful Item for Each Query"
excerpt: "Leetcode - 'Most Beautiful Item for Each Query' 문제 Java 풀이"
last_modified_at: 2024-11-13T18:30:00
header:
  image: /assets/images/leetcode/most-beautiful-item-for-each-query.png
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
[Link](https://leetcode.com/problems/most-beautiful-item-for-each-query/){:target="_blank"}

# 코드
```java
class Solution {

  public long countFairPairs(int[] nums, int lower, int upper) {
    Arrays.sort(nums);
    return this.countLess(nums, upper) - this.countLess(nums, lower - 1);
  }

  private long countLess(int[] nums, int sum) {
    long result = 0;
    int left = 0;
    int right = nums.length - 1;
    while (left < right) {
      if (nums[left] + nums[right] <= sum) {
        result += right - left++;
      } else {
        right--;
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/count-the-number-of-fair-pairs/submissions/1451454361/){:target="_blank"}

# 설명
1. nums 내 두 값의 합이 lower 이상, upper 이하인 조합의 갯수를 구하는 문제이다.

2. nums를 오름차순으로 정렬한다.

3. 4번에서 정의한 countLess(int[] nums, int sum) 메서드를 아래 두 값의 차잇값을 주어진 문제의 결과로 반환한다.
- sum에 upper를 넣어 수행한 결과인 값의 합이 upper 이하인 조합의 갯수.
- sum에 $lower - 1$을 넣어 수행한 결과인 값의 합이 $lower - 1$ 이하인 조합의 갯수.

4. nums 내 sum 이하까지 조합의 갯수를 계산하기 위한 countLess(int[] nums, int sum) 메서드를 정의한다.
- 메서드 풀이에 필요한 변수를 정의한다.
  - result는 갯수 계산에 필요한 변수로, 0으로 초기화한다.
  - left와 right는 nums의 좌측과 우측의 위치 값을 저장할 변수로, 0과 nums의 길이보다 1 작은 마지막 위치의 값으로 초기화한다.
- left가 right 미만일 때 까지 아래를 반복한다.
  - $nums[left] + nums[right]$의 결과가 sum 아래인 경우, result에 $right - left$인 가능한 범위 내 갯수를 더해준 후 left를 증가시켜준다.
  - 위의 결과가 아니라면 right를 감소시켜 범위를 좁혀준다.
- 반복이 완료되어 계산된 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountTheNumberoOfFairPairs.java){:target="_blank"}에서 확인 가능합니다.