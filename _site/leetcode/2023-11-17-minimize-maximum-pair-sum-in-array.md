---
title: "Leetcode Java Minimize Maximum Pair Sum in Array"
excerpt: "Leetcode Minimize Maximum Pair Sum in Array Java"
last_modified_at: 2023-11-17T22:40:00
header:
  image: /assets/images/leetcode/minimize-maximum-pair-sum-in-array.png
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
[Link](https://leetcode.com/problems/minimize-maximum-pair-sum-in-array){:target="_blank"}

# 코드
```java
class Solution {

  public int minPairSum(int[] nums) {
    Arrays.sort(nums);
    int result = 0;
    int length = nums.length;
    for (int i = 0; i < length / 2; i++) {
      result = Math.max(result, nums[i] + nums[length - i - 1]);
    }
    return result;
  }

}
```

# 결과
[Link](https://leetcode.com/problems/minimize-maximum-pair-sum-in-array/submissions/1101011886/){:target="_blank"}

# 설명
1. 정수 배열인 nums를 이용하여 아래의 조건을 만족하는 쌍들 중 합이 가장 큰 값을 구하는 문제이다.
- 각 정수는 하나의 쌍에만 속한다.
- 가장 큰 쌍의 합은 가장 작은 경우가 되어야 한다.

2. nums를 오름차순으로 정렬한다.

3. 문제 풀이에 필요한 변수를 정의한다.
- result는 쌍의 합이 가장 큰 값을 저장할 변수로, 0으로 초기화한다.
- length는 nums의 길이를 저장한 변수이다.

4. 0부터 $\frac{length}{2}$미만까지 i를 증가시키면서 result에 result와 현 위치에서 작은 값과 큰 값의 쌍을 묶은 합인 $nums[i] + nums[length - i - 1]$의 값 중 큰 값을 넣어준다.

5. 반복이 완료되면 쌍의 합이 가장 큰 값인 result를 주어진 문제의 결과로 반환한다.

# 소스
Sample Code는 [여기](https://github.com/GracefulSoul/leetcode/blob/master/src/main/java/gracefulsoul/problems/MinimizeMaximumPairSumInArray.java){:target="_blank"}에서 확인 가능합니다.