---
title: "Leetcode Java Maximum Gap"
excerpt: "Leetcode Maximum Gap Java 풀이"
last_modified_at: 2021-09-15T12:00:00
header:
  image: /assets/images/leetcode/maximum-gap.png
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
[Link](https://leetcode.com/problems/maximum-gap/){:target="_blank"}

# 코드
```java
class Solution {

  public int maximumGap(int[] nums) {
    int length = nums.length;
    if (length < 2) {
      return 0;
    }
    int min = nums[0];
    int max = nums[0];
    for (int num : nums) {
      min = Math.min(min, num);
      max = Math.max(max, num);
    }
    if (min == max) {
      return 0;
    }
    int gap = (int) Math.ceil((double) (max - min) / (length - 1));
    int bucketMin[] = new int[length];
    int bucketMax[] = new int[length];
    Arrays.fill(bucketMin, Integer.MAX_VALUE);
    Arrays.fill(bucketMax, Integer.MIN_VALUE);
    for (int num : nums) {
      int idx = (num - min) / gap;
      bucketMin[idx] = Math.min(bucketMin[idx], num);
      bucketMax[idx] = Math.max(bucketMax[idx], num);
    }
    for (int idx = 0; idx < bucketMin.length; ++idx) {
      if (bucketMin[idx] != Integer.MAX_VALUE) {
        gap = Math.max(gap, bucketMin[idx] - min);
        min = bucketMax[idx];
      }
    }
    return gap;
  }

}
```

# 결과
[Link](https://leetcode.com/submissions/detail/555079290/){:target="_blank"}

# 설명
1. 주어진 정수 배열 nums를 정렬된 상태의 인접한 두 값의 최대 차이를 구하는 문제이다.
- 단, 주어진 정수 배열 nums의 크기가 2 미만일 경우 주어진 문제의 결과로 0을 반환한다.
- 문제 풀이의 알고리즘은 [Linear time](https://en.wikipedia.org/wiki/Time_complexity#:~:text=An%20algorithm%20is%20said%20to%20take%20linear%20time%2C%20or%20O,the%20size%20of%20the%20input.&text=Linear%20time%20is%20the%20best,sequentially%20read%20its%20entire%20input.){:target="_blank"}으로 동작해야 하며, Linear extra space을 사용해야한다.

2. 주어진 배열 크기가 2 미만인 경우, 0을 주어진 문제의 결과로 반환한다.

3. 주어진 배열 nums의 값 중 최솟값과 최댓값을 저장하기 위한 min과 max를 정의하고, nums를 순회하여 min에 최솟값을, max에 최댓값을 넣어준다.

4. min과 max가 동일한 값일 경우 nums에 동일한 값들만 있을 경우이므로, 0을 주어진 문제의 결과로 반환한다.

5. 문제 풀이에 필요한 변수를 정의한다.
- gap은 최소 가능한 차이를 나타내며, $\frac{max - min}{length - 1}$의 값을 올림한 값을 저장한다.
- bucketMin과 bucketMax는 nums를 순회할 때 차이의 최솟값과 최댓값을 저장할 배열로, 주어진 배열 nums의 크기로 생성한다.

6. bucketMin에는 int형의 최댓값(2,147,483,647)을, bucketMax에는 int형의 최솟값(-2,147,483,648)을 채워준다.

7. 주어진 배열 nums를 반복하여 bucketMin과 bucketMax를 채워준다.
- 각 배열의 index를 저장할 idx에 $\frac{num - min}{gap}$의 값을 넣어준다.
- bucketMin[idx]에는 bucketMin[idx]와 num 중 작은 값을 넣어준다.
- bucketMax[idx]에는 bucketMax[idx]와 num 중 큰 값을 넣어준다.

8. bucketMin을 반복하여 nums 배열의 정렬된 상태에서의 인접한 두 값의 최대 차이를 구한다.
- bucketMin[idx]와 int형의 최댓값(2,147,483,647)이 아닌 경우만 아래를 수행한다.
  - gap에 gap과 $bucketMin[idx] - min$의 값 중 큰 값을 넣어준다.
  - min에는 bucketMax[idx] 값을 임시 저장시켜준다.

9. 반복이 완료되면 nums의 정렬된 상태의 인접한 두 값의 최대 차이를 저장한 gap을 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MaximumGap.java){:target="_blank"}에서 확인 가능합니다.