---
title: "Leetcode Java Range Sum Query - Immutable"
excerpt: "Leetcode - 'Range Sum Query - Immutable' 문제 Java 풀이"
last_modified_at: 2021-12-16T13:00:00
header:
  image: /assets/images/leetcode/range-sum-query-immutable.png
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
[Link](https://leetcode.com/problems/range-sum-query-immutable/){:target="_blank"}

# 코드
```java
class NumArray {

  private int[] nums;
  
  public NumArray(int[] nums) {
    int length = nums.length;
    this.nums = new int[length];
    for (int idx = 0; idx < length; idx++) {
      if (idx == 0) {
        this.nums[idx] = nums[idx];
      } else {
        this.nums[idx] = this.nums[idx - 1] + nums[idx];
      }
    }
  }

  public int sumRange(int left, int right) {
    if (left == 0) {
      return nums[right];
    } else {
      return nums[right] - nums[left - 1];
    }
  }

}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(left,right);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/602507642/){:target="_blank"}

# 설명
1. 배열을 주입하여 구간 값의 합을 구하는 NumArray 클래스를 완성하는 문제이다.
- 생성자인 NumArray(int[] nums)는 NumsArray 클래스를 초기화하여 nums의 값들을 주입한다.
- 메서드인 sumRange(int left, int right)는 생성자로 주입된 값들의 left번째 값부터 right번째 값까지 더하여 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums는 생성자로 부여된 정수들의 값을 누계하여 저장할 변수이다.

3. 생성자인 NumArray(int[] nums)를 완성한다.
- 주어진 nums의 길이를 length로 정의한다.
- 전역 변수인 nums를 nums의 길이로 초기화 한다.
- 반복을 이용하여 주입된 nums의 값의 idx번째 값까지 합을 전역변수 nums의 idx 위치의 값에 넣어준다.

4. 메서드인 sumRange(int left, int right)를 완성한다.
- nums에 각 위치 별 누계를 저장하였으므로 left가 0인 경우, nums[right]의 값이 이미 중촉하여 해당 값을 주어진 문제의 결과로 반환한다.
- left가 0이 아닌 경우, nums[right]의 값에서 nums[$left - 1$]의 값을 빼면 left번째 값에서 right번째 값들의 합이 되므로 뺀 값을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RangeSumQueryImmutable.java){:target="_blank"}에서 확인 가능합니다.