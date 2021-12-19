---
title: "Leetcode Java Range Sum Query - Mutable"
excerpt: "Leetcode Range Sum Query - Mutable Java 풀이"
last_modified_at: 2021-12-19T13:00:00
header:
  image: /assets/images/leetcode/range-sum-query-mutable.png
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
[Link](https://leetcode.com/problems/range-sum-query-mutable/){:target="_blank"}

# 코드
```java
class NumArray {

  private int[] nums;
  private int sum;

  public NumArray(int[] nums) {
    this.nums = nums;
    this.sum = 0;
    for (int num : nums) {
      this.sum += num;
    }
  }

  public void update(int index, int val) {
    this.sum -= this.nums[index] - val;
    this.nums[index] = val;
  }

  public int sumRange(int left, int right) {
    int temp = 0;
    if ((right - left) < this.nums.length / 2) {
      for (int idx = left; idx <= right; idx++) {
        temp += this.nums[idx];
      }
    } else {
      temp = this.sum;
      for (int idx = 0; idx < left; idx++) {
        temp -= this.nums[idx];
      }
      for (int idx = right + 1; idx < this.nums.length; idx++) {
        temp -= this.nums[idx];
      }
    }
    return temp;
  }

}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(index,val);
 * int param_2 = obj.sumRange(left,right);
 */
```

# 결과
[Link](https://leetcode.com/submissions/detail/603888213/){:target="_blank"}

# 설명
1. 배열을 주입하여 구간 값의 합을 구하거나 특정 위치의 값을 변경하는 NumArray 클래스를 완성하는 문제이다.
- 생성자인 NumArray(int[] nums)는 NumsArray 클래스를 초기화하여 nums의 값들을 주입한다.
- 메서드인 update(int index, int val)는 생성자로 주입된 값들의 index번째 값을 val 값으로 치환한다.
- 메서드인 sumRange(int left, int right)는 생성자로 주입된 값들의 left번째 값부터 right번째 값까지 더하여 반환한다.

2. 문제 풀이에 필요한 변수를 정의한다.
- nums는 생성자로 부여된 정수들의 값들을 넣을 변수이다.
- sum은 생성자로 부여된 정수들의 합을 넣을 변수이다.

3. 생성자인 NumArray(int[] nums)를 완성한다.
- 주어진 정수 배열인 nums를 전역 변수 nums에 주입한다.
- nums를 반복하여 모든 값들을 sum에 더해준다.

4. 메서드인 update(int index, int val)를 완성한다.
- 모든 값들의 합을 저장한 sum에 nums의 index번째 값과 val 값의 차이 값을 빼준다.
- nums의 index번째 위치에 val 값을 넣어준다.

5. 메서드인 sumRange(int left, int right)를 완성한다.
- 부분 합을 저장할 temp를 0으로 정의한다.
- $right - left$의 값이 nums의 길이 절반 미만인 경우, left 부터 right번째 값까지 순회하여 temp에 값을 더해준다.
- $right - left$의 값이 nums의 길이 절반 이상인 경우, 효율적으로 계산하기 위하여 아래를 수행한다.
  - 모든 값을 더한 sum의 값을 temp에 넣어준다.
  - nums의 처음부터 left까지, right부터 마지막까지 값을 temp에서 빼준다.
- 부분 합을 구한 temp를 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/RangeSumQuery2DImmutable.java){:target="_blank"}에서 확인 가능합니다.