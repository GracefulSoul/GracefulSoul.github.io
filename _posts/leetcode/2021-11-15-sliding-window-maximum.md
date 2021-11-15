---
title: "Leetcode Java Sliding Window Maximum"
excerpt: "Leetcode Sliding Window Maximum Java 풀이"
last_modified_at: 2021-11-15T12:00:00
header:
  image: /assets/images/leetcode/sliding-window-maximum.png
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
[Link](https://leetcode.com/problems/sliding-window-maximum/){:target="_blank"}

# 코드
```java
class Solution {

  public int[] maxSlidingWindow(int[] nums, int k) {
    int length = nums.length;
    int[] left = new int[length];
    int[] right = new int[length];
    for (int i = 0; i < length; i += k) {
      int max = Integer.MIN_VALUE;
      for (int j = i; j < i + k && j < length; j++) {
        max = Math.max(max, nums[j]);
        left[j] = max;
      }
    }
    int decrement = length % k == 0 ? k : length % k;
    for (int i = length - 1; i >= 0; i -= decrement, decrement = k) {
      int max = Integer.MIN_VALUE;
      for (int j = i; j > i - decrement && j >= 0; j--) {
        max = Math.max(max, nums[j]);
        right[j] = max;
      }
    }
    int[] result = new int[length - k + 1];
    for (int i = k - 1; i < length; i++) {
      if ((i + 1) % k == 0) {
        result[i - k + 1] = left[i];
      } else {
        result[i - k + 1] = Math.max(left[i], right[i - k + 1]);
      }
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/587459227/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums를 이용하여 k개 단위의 군집을 정해 해당 군집의 숫자 중 가장 큰 값을 모아 반환하는 문제이다.

2. 문제 풀이에 필요한 변수를 정의한다.
- length는 주어진 정수 배열 nums의 길이를 저장하기 위한 변수이다.
- left와 right는 좌측과 우측 기준에서 큰 값을 저장하기 위한 임시 변수이다.

3. 좌측 기준으로 nums의 크기 전까지 k 단위로 이동하면서 아래를 수행한다.
- 최대 값을 저장하기 위한 임시 변수인 max에 Integer의 최소값을 넣어준다.
- i부터 $i + k$와 nums의 크기 전까지 증가하면서 nums[j]와 max의 값 중 큰 값을 max에 넣고, left[j]에 해당 max 값을 넣어준다.

4. nums의 길이가 k의 배수인 경우 k를, 그렇지 않은 경우 nums의 길이에서 k를 나눈 나머지 값을 넣어준다.

5. 우측 기준으로 nums의 크기 부터 처음 값까지 decrement 단위로 이동하면서 아래를 수행한다.
- 최대 값을 저장하기 위한 임시 변수인 max에 Integer의 최소값을 넣어준다.
- i부터 $i - decrement$ 초과, 0 이상인 경우까지 점층적으로 감소시키며 반복하여 max와 nums[j]의 값 중 큰 값을 max에 넣고 right[j]에 해당 max 값을 넣어준다.

6. 결과를 저장할 result 배열을 $length - k + 1$ 크기로 정의한다.

7. $k - 1$부터 nums의 길이 만큼 점층적으로 증가시키며 반복하여 아래를 수행한다.
- $i + 1$의 값이 k의 배수인 경우 좌측 기준으로 최대 값을 정의한 left의 값이 정확하므로, result[$i - k + 1$]에 left[i]를 넣어준다.
- 그 외의 경우, left[i]와 right[$i - k + 1$]의 값 중 큰 값을 result[$i - k + 1$]에 넣어준다.

8. 반복이 종료되어 result에 모든 값이 채워지면 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/SlidingWindowMaximum.java){:target="_blank"}에서 확인 가능합니다.