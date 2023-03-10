---
title: "Leetcode Java Count of Range Sum"
excerpt: "Leetcode Count of Range Sum Java 풀이"
last_modified_at: 2022-01-03T13:00:00
header:
  image: /assets/images/leetcode/count-of-range-sum.png
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
[Link](https://leetcode.com/problems/count-of-range-sum/){:target="_blank"}

# 코드
```java
class Solution {

  public int countRangeSum(int[] nums, int lower, int upper) {
    int length = nums.length;
    long[] sum = new long[length + 1];
    for (int idx = 0; idx < length; idx++) {
      sum[idx + 1] = sum[idx] + nums[idx];
    }
    return this.recursive(sum, new long[length + 1], 0, length, lower, upper);
  }

  private int recursive(long[] sum, long[] cache, int low, int high, long lower, long upper) {
    if (low >= high) {
      return 0;
    }
    int mid = (high + 1 - low) / 2 + low;
    int count = this.recursive(sum, cache, low, mid - 1, lower, upper) + this.recursive(sum, cache, mid, high, lower, upper);
    int start = mid;
    int end = mid;
    for (int idx = low; idx < mid; idx++) {
      while (start <= high && sum[start] - sum[idx] < lower) {
        start++;
      }
      while (end <= high && sum[end] - sum[idx] <= upper) {
        end++;
      }
      count += end - start;
    }
    this.merge(sum, cache, low, mid, high);
    return count;
  }

  private void merge(long[] sum, long[] cache, int low, int mid, int high) {
    int left = low;
    int right = mid;
    int idx = low;
    while (left < mid && right <= high) {
      if (sum[left] <= sum[right]) {
        cache[idx++] = sum[left++];
      } else {
        cache[idx++] = sum[right++];
      }
    }
    while (left < mid) {
      cache[idx++] = sum[left++];
    }
    while (right <= high) {
      cache[idx++] = sum[right++];
    }
    System.arraycopy(cache, low, sum, low, high + 1 - low);
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/611895239/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums를 이용하여 주어진 정수 lower에서 upper 범위를 포함한 부분 범위 합의 개수를 반환하는 문제이다.
- 범위 합 S(i, j)는 i와 j를 포함한 nums 배열 내 값들의 합으로 정의된다. (단, i <= j이다.)

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 주어진 정수 배열 nums의 길이를 저장하는 변수이다.
- sum은 주어진 nums를 차례대로 합을 저장하는 배열로, nums를 순회하여 sum에 값을 누계하여 넣어준다.

3. 부분 범위 합의 개수를 세기 위한 recursive(long[] sum, long[] cache, int low, int high, long lower, long upper) 메서드를 완성한다.
- low가 high보다 크거나 같은 경우, 0을 반환한다.
- mid에 $\frac{high + 1 - low}{2} + low$의 값을 넣어준다.
- count는 $mid - 1$로 재귀호출한 값과 mid로 재귀호출한 값을 넣어준다.
- start와 end에 mid 값을 넣어준다.
- low부터 mid 전까지 idx를 증가시키며 반복시켜 아래를 수행한다.
  - high가 start보다 크거나 같고 $sum[start] - sum[idx]$ 값이 lower보다 작을때까지 반복하여 start를 증가시켜준다.
  - high가 end보다 크거나 같고 $sum[end] - sum[idx]$ 값이 upper보다 작거나 같을때까지 반복하여 end를 증가시켜준다.
  - 위의 반복이 완료되면 count에 $end - start$ 값을 넣어준다.
- 위의 반복이 완료되면 아래의 4번에서 정의한 merge(sum, cache, low, mid, high) 메서드를 호출하여 mergeSort를 수행하고 count를 반환한다.

4. 위의 mergeSort를 하기 위한 merge(long[] sum, long[] cache, int low, int mid, int high) 메서드를 완성한다.
- left와 idx에 low를, right에 mid 값을 넣어준다.
- left가 mid보다 작고 right가 high보다 같거나 작을때까지 반복하여 아래를 수행한다.
  - sum[left]의 값이 sum[right]값보다 작거나 같으면, cache[idx]에 sum[left] 값을 넣어주고 idx와 left를 증가시켜준다.
  - sum[left]의 값이 sum[right]값보다 크면, cache[idx]에 sum[right] 값을 넣어주고 idx와 right를 증가시켜준다.
- left가 mid보다 작을때까지 반복하여 cache[idx]에 sum[left] 값을 넣어주고 idx와 left를 증가시킨다.
- right가 high보다 작거나 같을때까지 반복하여 cache[idx]에 sum[right] 값을 넣어주고 idx와 right를 증가시킨다.
- cache의 low부터 $high + 1 - low$개의 값들을 sum의 low부터 차례대로 값을 넣어준다.

5. 3, 4번을 수행하여 확인한 부분 배열의 개수인 count를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/CountOfRangeSum.java){:target="_blank"}에서 확인 가능합니다.