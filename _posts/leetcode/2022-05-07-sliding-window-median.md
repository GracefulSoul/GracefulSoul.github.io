---
title: "Leetcode Java Sliding Window Median"
excerpt: "Leetcode Sliding Window Median Java 풀이"
last_modified_at: 2022-05-07T18:00:00
header:
  image: /assets/images/leetcode/sliding-window-median.png
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
[Link](https://leetcode.com/problems/sliding-window-median/){:target="_blank"}

# 코드
```java
class Solution {

  public double[] medianSlidingWindow(int[] nums, int k) {
    int[] part = new int[k];
    double[] result = new double[nums.length - k + 1];
    for (int i = 0; i < k; i++) {
      part[i] = nums[i];
    }
    Arrays.sort(part);
    result[0] = this.getMedian(part, k);
    for (int i = k, j = 1; i < nums.length; i++, j++) {
      this.delete(part, k, nums[i - k]);
      this.insert(part, k, nums[i]);
      result[j] = this.getMedian(part, k);
    }
    return result;
  }

  private double getMedian(int[] part, int k) {
    if (k % 2 == 1) {
      return (double) part[k / 2];
    } else {
      return (part[(k / 2) - 1] / 2.0) + (part[k / 2] / 2.0);
    }
  }

  private void delete(int[] part, int k, int value) {
    int left = 0;
    int right = k;
    while (left < right) {
      int mid = left + (right - left) / 2;
      if (part[mid] == value) {
        System.arraycopy(part, mid + 1, part, mid, k - (mid + 1));
        part[k - 1] = value;
        return;
      }
      if (part[mid] < value) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
  }

  private void insert(int[] part, int k, int value) {
    int left = 0;
    int right = k - 1;
    while (left < right) {
      int mid = left + (right - left) / 2;
      if (part[mid] < value) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    System.arraycopy(part, left, part, left + 1, (k - 1) - left);
    part[left] = value;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/694801030/){:target="_blank"}

# 설명
1. 정수의 배열인 nums를 이용하여 앞에서 부터 k개 씩 묶어 각각의 중앙값들을 찾아 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- part는 k개의 정수를 넣어 중앙값을 탐색하기 위한 배열로, k 크기로 정의하여 nums의 0 번째 값부터 k 번째 값까지 넣어준다.
- result는 각 중앙값을 넣을 배열로, $nums.length - k + 1$ 크기로 정의한다.
  - k개를 묶어 하나의 중앙값이 나오므로, 배열의 크기에서 $k - 1$을 뺀 값만큼 수의 중앙값이 나오게된다.
- part를 오름차순 정렬하고 result의 첫 값에 3번에서 정의한 getMedian(int[] part, int k) 메서드의 결과를 넣어준다.
- i는 k, j는 1부터 i가 nums의 길이 미만까지 i와 j를 증가시키며 아래를 수행한다.
  - 4번에서 정의한 delete(int[] part, int k, int value) 메서드를 수행하여 part에 nums의 $i - k$번째 값을 제거해준다.
  - 5번에서 정의한 insert(int[] part, int k, int value) 메서드를 수행하여 part에 nums의 i번째 값을 넣어준다.
  - result의 j번째 위치에 3번에서 정의한 getMedian(int[] part, int k) 메서드를 수행한 결과를 넣어준다.
- 반복이 완료되면 중앙값들을 넣은 result를 주어진 문제의 결과로 반환한다.

3. 중앙값을 계산하기 위한 getMedian(int[] part, int k) 메서드를 정의한다.
- k가 홀수인 경우, part의 $\frac{size}{2}$번째 값을 double 형으로 변환 후 반환한다.
- k가 짝수인 경우, part의 $\frac{size}{2} - 1$번째 값을 2.0으로 나눈 값과 part의 $\frac{size}{2}$번째 값을 2.0으로 나눈 값을 더해서 반환한다.

4. part 내 value에 대한 값을 제거하기 위한 delete(int[] part, int k, int value) 메서드를 정의한다.
- left를 0으로, right를 k로 넣어 초기화한다.
- left가 right보다 작을 때 까지 반복하여 아래를 수행한다.
  - mid에 $left + \frac{right - left}{2}$의 결과를 넣어 탐색 위치를 설정한다.
  - part의 mid번째 값이 value인 경우, part의 $mid + 1$번째 값부터 $k - (mid + 1)$개의 값들을 part의 mid번째 값 위치부터 넣어주고 part의 $k - 1$번째 값에 value를 넣어주고 수행을 멈춘다.
  - part의 mid번째 값이 value보다 작은 경우, left에 $mid + 1$을 넣고 아니면 right에 mid를 넣어 범위를 좁혀준다.

5. part 내 value를 넣기 위한 insert(int[] part, int k, int value) 메서드를 정의한다.
- left를 0으로, right를 $k - 1$로 넣어 초기화한다.
- left가 right보다 작을 때 까지 반복하여 아래를 수행한다.
  - mid에 $left + \frac{right - left}{2}$의 결과를 넣어 탐색 위치를 설정한다.
  - part의 mid번째 값이 value보다 작은 경우, left에 $mid + 1$을 넣고 아니면 right에 mid를 넣어 범위를 좁혀준다.
- 반복이 완료되면 part의 left 번째 값부터 $(k - 1) - left$번째 값까지 part의 $left + 1$번쨰 위치부터 넣어주고 part의 left번째 자리에 value를 넣어준다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SlidingWindowMedian.java){:target="_blank"}에서 확인 가능합니다.